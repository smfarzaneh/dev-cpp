# Setting up a C++ project with CMake

CMake is a software that automates a lot of mundane tasks in developing a C++ project. 
These include build, testing, packaging, and installation of your C++ software. 
CMake is cross-platform, free, and open source. 
I use CMake in nearly every C++ project I work on. 

## Directory structure
Assume that you are developing a C++ library named _MyProject_. 
This is the standard I follow to lay out the directory structure of the library. 
The root directory is lowercase version of the project name `myproject`. 
The source files (`*.hpp` and `*.cpp`) as well as unit tests (`*.test.cpp`) are located inside a subdirectory with the same name, `myproject/myproject`. 
The `app` folder contains the application source files. 
The `main.cpp` uses the `myproject` library to achieve some goal (e.g. demo for the library) or implement an application for the user. 
The CMake configurations are in the `CMakeLists.txt` file. 

```
myproject
|
├── myproject
|   ├── myclass.hpp
|   ├── myclass.cpp
|   └── myclass.test.cpp
|
├── app
|   └── main.cpp
|
└── CMakeLists.txt
```

## CMakeLists.txt
All the information that CMake needs about building, testing, packaging, and installing the software goes into the `CMakeLists.txt` file. 
Here is a template to start with. 

```cmake
# CMakeLists.txt

cmake_minimum_required(VERSION 3.29)

set(CMAKE_CXX_STANDARD 11)

project(MyProject VERSION 1.0.0 LANGUAGES CXX)

add_library(MyProject STATIC
    MyProject/myclass.cpp
)

target_include_directories(MyProject PUBLIC myproject/)

add_executable(MyProjectApp
    app/main.cpp
)

target_include_directories(MyProjectApp PUBLIC app/)


```

## Build
To build the project you can run the following commands in the root directory of the project `myproject/`. 

```bash
cmake -S . -B build/
cmake --build build/
./build/MyProjectApp
```

The first command configures the make files. The second command builds the `MyProject` library as well as the `MyProjectApp` application. The third line runs the application. 