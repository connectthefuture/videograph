
CMAKE_MINIMUM_REQUIRED(VERSION 2.6 FATAL_ERROR)
CMAKE_POLICY(VERSION 2.6)
IF(LUAROCKS_PREFIX)
    MESSAGE(STATUS "Installing Torch through Luarocks")
    STRING(REGEX REPLACE "(.*)lib/luarocks/rocks.*" "\\1" CMAKE_INSTALL_PREFIX  "${LUAROCKS_PREFIX}")
    MESSAGE(STATUS "Prefix inferred from Luarocks: ${CMAKE_INSTALL_PREFIX}")
ENDIF()
FIND_PACKAGE(Torch REQUIRED)
FIND_PACKAGE(Boost REQUIRED)

SET(src init.cpp)
SET(luasrc init.lua)

ADD_TORCH_PACKAGE(videograph "${src}" "${luasrc}" "Video Processing")
TARGET_LINK_LIBRARIES(videograph luaT TH)
