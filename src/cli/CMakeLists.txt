# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at http://mozilla.org/MPL/2.0/.

set(CMAKE_SKIP_BUILD_RPATH FALSE)
set(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE)
list( APPEND CMAKE_INSTALL_RPATH "\$ORIGIN/../lib64" )

add_executable(lsb_heka_cat lsb_heka_cat)
target_link_libraries(lsb_heka_cat luasandboxutil)

if(LIBM_LIBRARY)
  target_link_libraries(lsb_heka_cat ${LIBM_LIBRARY})
endif()

install(TARGETS lsb_heka_cat DESTINATION ${CMAKE_INSTALL_BINDIR})
