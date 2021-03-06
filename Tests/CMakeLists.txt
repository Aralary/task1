cmake_minimum_required(VERSION 3.14)
project(Tests)

set(CMAKE_CXX_STANDARD 17)
string(APPEND CMAKE_CXX_FLAGS " -fprofile-arcs -ftest-coverage -O0")
if (BUILD_SANITIZERS)
    string(APPEND CMAKE_CXX_FLAGS " -fsanitize=address")
endif()
string(APPEND CMAKE_EXE_LINKER_FLAGS " -coverage -lgcov")
#set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-fprofile-arcs -ftest-coverage -O0")
#set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -coverage -lgcov")
#string(APPEND ${CMAKE_CXX_FLAGS} " -fsanitize=address,undefined -fno-sanitize-recover=all -fsanitize-undefined-trap-on-error")
file(GLOB SOURCES *.cpp)
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTest gtest_main)

add_executable(${PROJECT_NAME} ${SOURCES})
target_include_directories(${PROJECT_NAME} PUBLIC ${AREA_LIB_INCLUDE_DIRS} ${GTest_INCLUDE_DIRECTORIES})
target_link_libraries(${PROJECT_NAME} ${AREA_LIB_LIBRARIES} ${GTest_LIBRARIES})
