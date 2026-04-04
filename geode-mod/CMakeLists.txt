cmake_minimum_required(VERSION 3.21)
project(gd-vulkan-switcher CXX)

set(GEODE_SDK "${CMAKE_SOURCE_DIR}/vendor/geode" CACHE PATH "Path to Geode SDK")
list(APPEND CMAKE_MODULE_PATH "${GEODE_SDK}/cmake/")
include(GeodeSDK)

file(GLOB_RECURSE SOURCES "src/*.cpp")

# Geode Mod as shared Lib
add_library(gd-vulkan-switcher SHARED ${SOURCES})

target_include_directories(gd-vulkan-switcher
    PRIVATE
        include/
        ../shared/include/
)

target_link_libraries(gd-vulkan-switcher
    PRIVATE
        geode-sdk
)

setup_geode_mod(gd-vulkan-switcher)
