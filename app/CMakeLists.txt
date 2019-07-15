# For more information about using CMake with Android Studio, read the


# documentation: https://d.android.com/studio/projects/add-native-code.html


# Sets the minimum version of CMake required to build the native library.


cmake_minimum_required(VERSION 3.6)


# Creates and names a library, sets it as either STATIC


# or SHARED, and provides the relative paths to its source code.


# You can define multiple libraries, and CMake builds them for you.


# Gradle automatically packages shared libraries with your APK.


add_library(
#外部引入的名称
opencv_java4
SHARED
IMPORTED)


set_target_properties(
opencv_java4
PROPERTIES IMPORTED_LOCATION
../../../../src/main/jniLibs/armeabi-v7a/libopencv_java4.so)


#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")


if(CMAKE_COMPILER_IS_GNUCXX)


set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")


message(STATUS "optional:-std=c++11")


endif(CMAKE_COMPILER_IS_GNUCXX)

include_directories(src/main/cpp)
include_directories(src/main/jniLibs/include)


add_library( # Sets the name of the library.


detection_based_tracker


# Sets the library as a shared library.


SHARED


# Provides a relative path to your source file(s).


src/main/cpp/DetectionBasedTracker_jni.cpp )


# Searches for a specified prebuilt library and stores the path as a


# variable. Because CMake includes system libraries in the search path by


# default, you only need to specify the name of the public NDK library


# you want to add. CMake verifies that the library exists before


# completing its build.


find_library( # Sets the name of the path variable.


log-lib


# Specifies the name of the NDK library that


# you want CMake to locate.


log )


# Specifies libraries CMake should link to your target library. You


# can link multiple libraries, such as libraries you define in this


# build script, prebuilt third-party libraries, or system libraries.


target_link_libraries( # Specifies the target library.


detection_based_tracker opencv_java4


# Links the target library to the log library


# included in the NDK.


${log-lib} )