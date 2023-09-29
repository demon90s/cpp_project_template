cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

set(PROJECT "main")

project(${PROJECT})

message(STATUS "[DEBUG] cmake running on system ${CMAKE_SYSTEM_NAME}")

set(LIBS "")
if (CMAKE_SYSTEM_NAME STREQUAL "Linux")
    # Linux
    set(CMAKE_CXX_COMPILE_FLAGS "${CMAKE_CXX_COMPILE_FLAGS} -g -Wall -O2 -std=c++11")
elseif (CMAKE_SYSTEM_NAME STREQUAL "Windows")
    # Windows
    #add_definitions(/wd"4996" /wd"4819" /wd"4129")
    set_property(DIRECTORY PROPERTY VS_STARTUP_PROJECT ${PROJECT})
endif()

include_directories(${PROJECT_SOURCE_DIR}/include
	${PROJECT_SOURCE_DIR}/src)
link_directories(${PROJECT_SOURCE_DIR}/lib)

file(GLOB_RECURSE SRC_FILES ${PROJECT_SOURCE_DIR}/src/*)
source_group(TREE ${PROJECT_SOURCE_DIR} FILES ${SRC_FILES})

add_executable(${PROJECT} ${SRC_FILES})
target_link_libraries(${PROJECT} ${LIBS})
