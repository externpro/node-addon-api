cmake_minimum_required(VERSION 3.31)
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/.devcontainer/cmake)
include(preproject)
project(node-addon-api VERSION 3.0.2.1)
include(flags)
include(GNUInstallDirs)
set(XP_INSTALL_CMAKEDIR ${CMAKE_INSTALL_DATADIR}/cmake) # xpPackageDevel
set(XP_NAMESPACE xpro)
set(targetsFile ${PROJECT_NAME}-targets)
set(lib_name ${PROJECT_NAME})
xpFindPkg(PKGS nodexp)
xpPackageDevel(TARGETS_FILE ${targetsFile} DEPS nodexp LIBRARIES ${XP_NAMESPACE}::${lib_name})
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
target_link_libraries(${lib_name} INTERFACE ${XP_NAMESPACE}::node)
########################################
install(TARGETS ${lib_name} EXPORT ${targetsFile})
install(FILES ${libsrcs} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})
install(EXPORT ${targetsFile} DESTINATION ${XP_INSTALL_CMAKEDIR} NAMESPACE ${XP_NAMESPACE}::)
install(FILES CHANGELOG.md LICENSE.md README.md DESTINATION ${CMAKE_INSTALL_DATADIR})
install(DIRECTORY doc DESTINATION ${CMAKE_INSTALL_DATADIR})
