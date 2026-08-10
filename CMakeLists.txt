cmake_minimum_required(VERSION 3.10)

project(VulkanTuts LANGUAGES CXX)


find_package(SDL3 REQUIRED)
find_package(Vulkan REQUIRED COMPONENTS volk shaderc_combined)
find_package(glm REQUIRED)

set(CMAKE_CXX_STANDARD 26)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_DIR "${CMAKE_SOURCE_DIR}/src")

file(GLOB ENGINE_SOURCES CONFIGURE_DEPENDS "${SRC_DIR}/*.cpp")

add_executable(VulkanTuts)

if(MSVC)
    target_compile_options(VulkanTuts PRIVATE /std:c++latest)
endif()
target_sources(VulkanTuts PRIVATE ${ENGINE_SOURCES})

target_link_libraries(VulkanTuts PRIVATE
        Vulkan::Vulkan
        Vulkan::volk
        Vulkan::shaderc_combined
        glm::glm
        SDL3::SDL3
)
