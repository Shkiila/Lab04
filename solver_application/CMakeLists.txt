cmake_minimum_required(VERSION 3.4)
project(solver)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib)  
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib solver_lib)  
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib)

add_executable(solver equation.cpp)
target_link_libraries(solver formatter_ex solver_lib)