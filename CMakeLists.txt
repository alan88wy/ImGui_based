# ----- 1. Runtime requirement 

cmake_minimum_required(VERSION 3.15)


if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug CACHE STRING "" FORCE)
endif()

set(CMAKE_CXX_STANDARD 23)
set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DVK_PROTOTYPES")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DVK_PROTOTYPES")

# ----- 2. Debugging

# ----- 3. Global variable

set(this Hello)

project(${this} CXX C)



# ----- 4. Software tool

# ----- 5. Library

set(includes ${CMAKE_CURRENT_SOURCE_DIR}/imgui )
include_directories( ${includes} )

set( sources ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp)

# set(VULKAN_LIB_LIST "vulkan-1")

set(VENDORS "./imgui")

file(GLOB PROJECT_HEADERS imgui/*.h)
file(GLOB PROJECT_SOURCES *.cpp imgui/*.cpp)

source_group("Headers" FILES ${PROJECT_HEADERS})
# source_group("Shaders" FILES ${PROJECT_SHADERS})
source_group("Sources" FILES ${PROJECT_SOURCES})
# source_group("Vendors" FILES ${VENDORS_SOURCES})

# ----- 6. Compile

# add_executable( ${this} ${sources} )
add_executable(${this} ${PROJECT_SOURCES} ${PROJECT_HEADERS} )


find_package(fmt REQUIRED)
find_package(range-v3 REQUIRED)
find_package(cxxopts REQUIRED)
find_package(glfw3 REQUIRED)
find_package(glm REQUIRED)
find_package(GLUT REQUIRED)
find_package(vulkan REQUIRED)

target_link_libraries( ${this} PUBLIC ${target_lib} ) 
target_include_directories( ${this} PUBLIC ${includes} ) 
target_link_libraries(${this}
  PRIVATE
    fmt::fmt
    range-v3::range-v3
    cxxopts::cxxopts
    glfw
    glm::glm
    GLUT::GLUT
    Vulkan::Vulkan
)