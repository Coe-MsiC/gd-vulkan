cmake_minimum_required(VERSION 3.21)
project(gd-vulkan CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Vulkan SDK must be installed
find_package(Vulkan REQUIRED)

# Vendor-Libs
add_subdirectory(vendor/VulkanMemoryAllocator)
add_subdirectory(vendor/shaderc EXCLUDE_FROM_ALL)

# Subprojects
add_subdirectory(vulkan-renderer)
add_subdirectory(geode-mod)
