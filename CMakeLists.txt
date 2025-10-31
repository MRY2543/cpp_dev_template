cmake_minimum_required(VERSION 3.10)
# set toolchain
set(CMAKE_TOOLCHAIN_FILE "/opt/vcpkg/scripts/buildsystems/vcpkg.cmake" CACHE STRING "Vcpkg toolchain file")
project(HelloWorld)

set(CMAKE_CXX_STANDARD 17)
add_executable(${PROJECT_NAME} helloworld.cpp)

#---------- Link lib ------------
find_package(fmt CONFIG REQUIRED)
find_package(jsoncpp CONFIG REQUIRED)
find_package(jwt-cpp CONFIG REQUIRED)
find_package(Boost REQUIRED)
message(STATUS "library Boost dir\t: ${Boost_INCLUDE_DIRS}")

target_link_libraries(${PROJECT_NAME} PRIVATE 
    fmt::fmt 
    JsonCpp::JsonCpp
    jwt-cpp::jwt-cpp
    ${Boost_LIBRARIES}
)

#-------------- BUILD Release --------------------------------
if(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3")
endif()