cmake_minimum_required(VERSION 3.17)
project(imgui)

# Get Backend Files
file (GLOB BACKEND_FILES "backends/imgui_impl_vulkan.cpp" 
    "backends/imgui_impl_vulkan.h"
    "backends/imgui_impl_glfw.h"
    "backends/imgui_impl_glfw.cpp"
)

# Get Vulkan
find_package(Vulkan REQUIRED)

# Imgui Files
file (GLOB SRC_FILES  "*.cpp" "*.h")

# Misc Files
file (GLOB MISC_FILES "misc/cpp/*.cpp" "misc/cpp/*.h")

# Create Library
add_library(${PROJECT_NAME} STATIC ${BACKEND_FILES} ${SRC_FILES} ${MISC_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC "./" ${Vulkan_INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME} glfw)