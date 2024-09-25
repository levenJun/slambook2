cmake_minimum_required(VERSION 2.8)
project(dense_monocular)

# set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++11 -march=native -O3")

if(CMAKE_BUILD_TYPE MATCHES "Debug")
        MESSAGE("build by Debug")
    set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -O0 -g -fstack-protector -fsanitize=address -fno-omit-frame-pointer")
endif()

############### dependencies ######################
# Eigen
# include_directories("/usr/include/eigen3")
find_package(Eigen3 3.1.0 REQUIRED)
# OpenCV
find_package(OpenCV 3.4 REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
# Sophus
# find_package(Sophus REQUIRED)
# include_directories(${Sophus_INCLUDE_DIRS})
include_directories(
        ${PROJECT_SOURCE_DIR}/../../Thirdparty/Sophus
        ${EIGEN3_INCLUDE_DIR}
        )

set(THIRD_PARTY_LIBS
        ${OpenCV_LIBS}
        # ${Sophus_LIBRARIES}
        )

add_executable(dense_mapping dense_mapping.cpp)
target_link_libraries(dense_mapping ${THIRD_PARTY_LIBS})