cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_STANDARD 17)

set(HUNTER_CACHE_SERVERS
    "https://github.com/bmstu-iu8-cpp-sem-3/hunter-cache"
    CACHE STRING "Default cache server")

include("cmake/HunterGate.cmake")

huntergate(URL "https://github.com/cpp-pm/hunter/archive/v0.23.314.tar.gz" SHA1
           "95c47c92f68edb091b5d6d18924baabe02a6962a")

project(builder)

hunter_add_package(Boost COMPONENTS filesystem system program_options)
hunter_add_package(BoostProcess)

find_package(Boost COMPONENTS filesystem system program_options REQUIRED)
find_package(BoostProcess CONFIG REQUIRED)

add_executable(builder ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp)

target_link_libraries(builder Boost::filesystem Boost::system BoostProcess::boost_process Boost::program_options)

install(TARGETS builder RUNTIME DESTINATION bin)
