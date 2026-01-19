cmake_minimum_required(VERSION 3.31)
set(CMAKE_PROJECT_TOP_LEVEL_INCLUDES .devcontainer/cmake/xproinc.cmake)
project(node-addon-api VERSION 8.5.0)
set(targetsFile ${PROJECT_NAME}-targets)
set(lib_name ${PROJECT_NAME})
xpFindPkg(PKGS nodexp)
if(DEFINED XP_NAMESPACE)
  xpExternPackage(NAMESPACE ${XP_NAMESPACE}
    TARGETS_FILE ${targetsFile} LIBRARIES ${lib_name}
    BASE v${CMAKE_PROJECT_VERSION} XPDIFF "intro" DEPS nodexp
    WEB "https://github.com/nodejs/node-addon-api" UPSTREAM "github.com/nodejs/node-addon-api"
    DESC "Module for using N-API from C++"
    LICENSE "[MIT](https://github.com/nodejs/node-addon-api/blob/v8.5.0/LICENSE.md 'MIT License')"
    )
  set(CMAKE_INSTALL_CMAKEDIR ${XP_INSTALL_CMAKEDIR})
  set(nameSpace NAMESPACE ${XP_NAMESPACE}::)
elseif(NOT DEFINED CMAKE_INSTALL_CMAKEDIR)
  set(CMAKE_INSTALL_CMAKEDIR ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})
endif()
########################################
set(libsrcs
  napi-inl.deprecated.h
  napi-inl.h
  napi.h
  )
########################################
add_library(${lib_name} INTERFACE ${libsrcs})
target_include_directories(${lib_name} INTERFACE $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)
target_compile_definitions(${lib_name} INTERFACE NODE_ADDON_API_DISABLE_DEPRECATED NAPI_CPP_EXCEPTIONS)
target_link_libraries(${lib_name} INTERFACE ${NODEXP_LIBRARIES})
########################################
install(TARGETS ${lib_name} EXPORT ${targetsFile})
install(FILES ${libsrcs} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})
install(EXPORT ${targetsFile} DESTINATION ${CMAKE_INSTALL_CMAKEDIR} ${nameSpace})
install(FILES CHANGELOG.md LICENSE.md README.md DESTINATION ${CMAKE_INSTALL_DATADIR})
install(DIRECTORY doc DESTINATION ${CMAKE_INSTALL_DATADIR})
