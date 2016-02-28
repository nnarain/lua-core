
cmake_minimum_required(VERSION 2.8.3)

project(lua)
set(LUA_VERSION 5.2)

set(LUA_CORE
	src/lapi.c
	src/lcode.c
	src/lctype.c
	src/ldebug.c
	src/ldo.c
	src/ldump.c
	src/lfunc.c
	src/lgc.c
	src/llex.c
	src/lmem.c
	src/lobject.c
	src/lopcodes.c
	src/lparser.c
	src/lstate.c
	src/lstring.c
	src/ltable.c
	src/ltm.c
	src/lundump.c
	src/lvm.c
	src/lzio.c
)

set(LUA_LIB
	src/lauxlib.c
	src/lbaselib.c
	src/lbitlib.c
	src/lcorolib.c
	src/ldblib.c
	src/liolib.c
	src/lmathlib.c
	src/loslib.c
	src/lstrlib.c
	src/ltablib.c
	src/loadlib.c
	src/linit.c
)

include_directories(
	include/
)

# lua as ansi c
add_definitions(-DLUA_ANSI -DLUA_COMPAT_ALL)

# build lua static library
add_library(lua STATIC
	${LUA_CORE}
	${LUA_LIB}
)

# build lua executable
add_executable(lua-${LUA_VERSION}
	src/lua.c
)
target_link_libraries(lua-${LUA_VERSION} lua m)

# build lua compiler
add_executable(luac-${LUA_VERSION}
	src/luac.c
)
target_link_libraries(luac-${LUA_VERSION} lua m)

# install
install(
	TARGETS
		lua-${LUA_VERSION}
		luac-${LUA_VERSION}
		lua
)