cmake_minimum_required(VERSION 3.9)

project(anomaly)

find_package(OpenMP)
if (OPENMP_FOUND)
    list(APPEND CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    list(APPEND CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()

set(CMAKE_CXX_STANDARD 17)

if (CMAKE_COMPILER_IS_GNUCXX)
elseif (MSVC)
    add_definitions(-D_USE_MATH_DEFINES -DNOMINMAX)
endif()

find_package(OpenCV REQUIRED)
find_package(Eigen3 REQUIRED)

set(SOURCE_FILES src/gem.cpp src/gem.cpp)
set(HEADER_FILES src/include/gem.h src/include/lambert.h src/include/pca.h src/include/suv.h)

add_executable(${PROJECT_NAME} ${SOURCE_FILES} ${HEADER_FILES} src/anomaly_detector.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE ${OpenCV_INCLUDE_DIRS})
target_include_directories(${PROJECT_NAME} PRIVATE ${EIGEN3_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} Eigen3::Eigen)

#add_executable(generate_dataset ${SOURCE_FILES} ${HEADER_FILES} src/generate_dataset.cpp)
#target_include_directories(generate_dataset PRIVATE ${OpenCV_INCLUDE_DIRS})
#target_include_directories(generate_dataset PRIVATE ${EIGEN3_INCLUDE_DIR})
#target_link_libraries(generate_dataset ${OpenCV_LIBS} Eigen3::Eigen)
