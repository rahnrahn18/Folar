cmake_minimum_required(VERSION 3.10.2)

# Project name
project("folar-native")

# Use C++ 17
set(CMAKE_CXX_STANDARD 17)

# Set path to OpenCV directory
# Relative to app/src/main/jni
set(OPENCV_ROOT ${CMAKE_CURRENT_SOURCE_DIR}/../../../../opencv)

# Include OpenCV headers
include_directories(${OPENCV_ROOT}/native/jni/include)

# Import the prebuilt OpenCV library
add_library(lib_opencv SHARED IMPORTED)

# Set the location of the prebuilt library
set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION
    ${OPENCV_ROOT}/src/main/jniLibs/${ANDROID_ABI}/libopencv_java4.so)

# Create the native library for the app
add_library(folar-native SHARED
    NativeBridge.cpp
)

# Link libraries
target_link_libraries(folar-native
    lib_opencv
    log
    android
    jnigraphics
)
