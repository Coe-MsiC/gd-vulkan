cmake_minimum_required(VERSION 3.21)
project(opengl32 CXX)

# All ource files
file(GLOB_RECURSE SOURCES "src/*.cpp")

# create dll
add_library(opengl32 SHARED ${SOURCES})

# DEF-file for correct DLL-Exports
target_sources(opengl32 PRIVATE exports/opengl32.def)

target_include_directories(opengl32
    PRIVATE
        include/
        ${Vulkan_INCLUDE_DIRS}
        ../shared/include/
        ../vendor/VulkanMemoryAllocator/include/
        ../vendor/shaderc/libshaderc/include/
)

target_link_libraries(opengl32
    PRIVATE
        ${Vulkan_LIBRARIES}
        VulkanMemoryAllocator
        shaderc_combined      # static - no extra dll
        dwmapi.lib            # for HWND/Surface
)

# Release-Build optimizations
target_compile_options(opengl32 PRIVATE
    $<$<CONFIG:Release>:/O2 /GL>
)

# Outputs as "opengl32.dll" directly (not as "libopengl32.dll")
set_target_properties(opengl32 PROPERTIES
    OUTPUT_NAME "opengl32"
    PREFIX ""
)
