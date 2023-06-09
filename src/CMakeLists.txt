# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at http://mozilla.org/MPL/2.0/.

if(MSVC)
	add_definitions(
	-DLUA_BUILD_AS_DLL
	-D_CRT_SECURE_NO_WARNINGS
	)
else()
	add_definitions(
	-DLUA_USE_POSIX 
	-DLUA_USE_DLOPEN 
	-DLUA_USE_STRTODHEX
	-DLUA_USE_LONGLONG 
	-DLUA_USE_GMTIME_R
	)
endif()

set(LUA_SANDBOX_SRC
luasandbox.c
luasandbox_output.c
luasandbox_serialize.c
)

add_library(luasandbox SHARED ${LUA_SANDBOX_SRC})
set_target_properties(luasandbox PROPERTIES VERSION ${PROJECT_VERSION} SOVERSION 0)
target_link_libraries(luasandbox luasandboxutil luajit-5.1 m dl ${CMAKE_DL_LIBS} c)
#if(LIBM_LIBRARY)
#  target_link_libraries(luasandbox ${LIBM_LIBRARY})
#endif()
install(TARGETS luasandbox DESTINATION ${CMAKE_INSTALL_LIBDIR})

add_subdirectory(util)
add_subdirectory(heka)
if(NOT WIN32) # todo need to add getopt support for Windows
  add_subdirectory(cli)
endif()
add_subdirectory(test)
