# TIMP_Lab4
## CMake Files
```
cmake_minimum_required(VERSION 3.4)
project(formatter)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter STATIC formatter.cpp formatter.h)
```
```
cmake_minimum_required(VERSION 3.4)
project(formatter_ex_lib)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter_ex_lib STATIC formatter_ex.cpp )
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib formatter)  
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib)
target_link_libraries(formatter_ex_lib formatter)
```
```
cmake_minimum_required(VERSION 3.4)
project(hello_world)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib)  
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib)

add_executable(hello_world hello_world.cpp)
target_link_libraries(hello_world formatter_ex_lib)
```
```
cmake_minimum_required(VERSION 3.4)
project(solver_lib)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(solver_lib STATIC solver.cpp solver.h)
```
```
cmake_minimum_required(VERSION 3.4)
project(solver)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib)  
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib solver_lib)  
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib)

add_executable(solver equation.cpp)
target_link_libraries(solver formatter_ex_lib)
target_link_libraries(solver solver_lib)
```

## .yml File
```
name: CMake

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

env:
  BUILD_TYPE: Release

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Create and build formatter_lib
      working-directory: formatter_lib
      run: cmake -H. -Bbuild
      run: cmake --build build
    
    - name: Create and build formatter_ex_lib
      working-directory: formatter_ex_lib
      run: cmake -H. -Bbuild
      run: cmake --build build
    
    - name: Create and build hello_world_application
      working-directory: hello_world_application
      run: cmake -H. -Bbuild
      run: cmake --build build
    
    - name: Create and build solver_lib
      working-directory: solver_lib
      run: cmake -H. -Bbuild
      run: cmake --build build
    
    - name: Create and build solver_application
      working-directory: solver_application
      run: cmake -H. -Bbuild
      run: cmake --build build
 ```
