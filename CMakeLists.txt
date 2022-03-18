cmake_minimum_required(VERSION 3.17)
project(imgui)


# Imgui Files
file (GLOB SRC_FILES  "*.cpp" "*.h")

# Misc Files
file (GLOB MISC_FILES "misc/cpp/*.cpp" "misc/cpp/*.h")


if (WIN32 OR (UNIX AND NOT APPLE))
    # Get Vulkan
    find_package(Vulkan REQUIRED)

    # Get Backend Files
    file (GLOB BACKEND_FILES "backends/imgui_impl_vulkan.cpp" 
        "backends/imgui_impl_vulkan.h"
        "backends/imgui_impl_glfw.h"
        "backends/imgui_impl_glfw.cpp"
    )

	if (WIN32)
		message(STATUS "Compiling imgui for windows")
        set(INCLUDE_DIRS ${Vulkan_INCLUDE_DIRS})
	else()
		message(STATUS "Compiling imgui for linux")
	endif()
endif()

if (APPLE)
	message(STATUS "Compiling imgui for apple")
endif()



# Create Library
add_library(${PROJECT_NAME} STATIC ${BACKEND_FILES} ${SRC_FILES} ${MISC_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC "./" ${INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME} glfw)
