# set minimum required version for cmake
cmake_minimum_required(VERSION 3.14)

# define project name
set(project_name "MelaniQtCv")

# set project name
project("${project_name}")


set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

# this is a c++11 project
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# add Qt package to the project
find_package(QT NAMES Qt6 Qt5 COMPONENTS Core REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core REQUIRED)

# add opencv package to the project
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
set(OpenCV_LIBRARIES ${OpenCv_LIBS})

# print opencv version infomation
message(STATUS "    version: ${OpenCV_VERSION}")

# add execurable
add_executable(Opencv
  main.cpp
)

# link libraries
target_link_libraries(Opencv Qt${QT_VERSION_MAJOR}::Core ${OpenCV_LIBS})

# copy required images to directory with executable
set(IMAGES ${CMAKE_SOURCE_DIR}/images/puppy.bmp)
file(COPY ${IMAGES} DESTINATION .)
