cmake_minimum_required(VERSION 3.20)

project(clarity_interpreter)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED true)

include(ExternalProject)
ExternalProject_Add(spdlog
	PREFIX spdlog
	SOURCE_DIR ${PROJECT_SOURCE_DIR}/lib/spdlog
	CMAKE_ARGS -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
	-DCMAKE_CXX_COMPILER=${CMAKE_CXX_COMPILER}
	-DCMAKE_C_COMPILER=${CMAKE_C_COMPILER}
	-DCMAKE_TOOLCHAIN_FILE=${CMAKE_TOOLCHAIN_FILE}
	-DCMAKE_INSTALL_PREFIX=${STAGING_DIR}
	-DSPDLOG_BUILD_SHARED=OFF
)

set(CLARITY_SRC_DIR ./src)
set(CLARITY_INC_DIR ./include)

set(CLARITY_SRC
	${CLARITY_SRC_DIR}/main.cpp
)

add_executable(clarity_interpreter ${CLARITY_SRC})
add_dependencies(clarity_interpreter spdlog)
target_include_directories(clarity_interpreter PUBLIC ${STAGING_DIR}/include/)