cmake_minimum_required(VERSION 4.3)
project(node-addon-api VERSION 8.5.0)
########################################
set(libsrcs
  napi-inl.deprecated.h
  napi-inl.h
  napi.h
  )
########################################
set(lib_name ${PROJECT_NAME})
add_library(${lib_name} INTERFACE ${libsrcs})
target_include_directories(${lib_name} INTERFACE $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)
target_compile_definitions(${lib_name} INTERFACE NODE_ADDON_API_DISABLE_DEPRECATED NAPI_CPP_EXCEPTIONS)
find_package(nodexp REQUIRED)
target_link_libraries(${lib_name} INTERFACE ${NODEXP_LIBRARIES})
########################################
set(targetsFile ${PROJECT_NAME}-targets)
if(COMMAND xpExternPackage)
  xpExternPackage(TARGETS_FILE ${targetsFile}
    LIBRARIES ${lib_name} DEFAULT_TARGETS ${lib_name}
    BASE v${CMAKE_PROJECT_VERSION} XPDIFF "intro"
    WEB "https://github.com/nodejs/node-addon-api" UPSTREAM "github.com/nodejs/node-addon-api"
    DESC "Module for using N-API from C++"
    LICENSE "[MIT](https://github.com/nodejs/node-addon-api/blob/v8.5.0/LICENSE.md 'MIT License')"
    )
elseif(NOT DEFINED CMAKE_INSTALL_CMAKEDIR)
  set(CMAKE_INSTALL_CMAKEDIR ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})
endif()
########################################
install(TARGETS ${lib_name} EXPORT ${targetsFile})
install(FILES ${libsrcs} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})
install(EXPORT ${targetsFile} DESTINATION ${CMAKE_INSTALL_CMAKEDIR} NAMESPACE ${PROJECT_NAME}::)
install(FILES CHANGELOG.md LICENSE.md README.md DESTINATION ${CMAKE_INSTALL_DATADIR})
install(DIRECTORY doc DESTINATION ${CMAKE_INSTALL_DATADIR})
