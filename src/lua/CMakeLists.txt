
set(INSTALL_LUA_ROOT ${INSTALL_DATADIR}/lua)
set(INSTALL_LUA_INIT ${INSTALL_LUA_ROOT}/init.lua)
set(INSTALL_LUA_CORE ${INSTALL_LUA_ROOT}/core)
set(INSTALL_LUA_LIBS ${INSTALL_LUA_ROOT}/lib)
set(INSTALL_LUA_THIRD_PARTY ${INSTALL_LUA_ROOT}/third-party)
set(INSTALL_LUA_SCRIPTS ${INSTALL_LUA_ROOT}/scripts)

configure_file(ec_lua_config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/include/ec_lua_config.h)

# Take care of building our C-based stuff.
include_directories(${CMAKE_CURRENT_BINARY_DIR}/include)
include_directories(${LUAJIT_INCLUDE_DIR})
add_library(ec_lua ec_lua.c)
SET_TARGET_PROPERTIES(ec_lua PROPERTIES COMPILE_FLAGS -fPIC)
add_dependencies(ec_lua luajit)
#target_link_libraries(ec_lua ${LUAJIT_LIBRARY})

# Add our 'shared' code. 
add_subdirectory(share)
