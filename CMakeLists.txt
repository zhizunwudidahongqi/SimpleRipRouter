cmake_minimum_required(VERSION 2.8)
project(ROUTER_LAB LANGUAGES C CXX)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)

set(BACKEND LINUX CACHE STRING "Router platform")
set(BACKEND_VALUES "LINUX" "XILINX" "MACOS" "STDIO")
set_property(CACHE BACKEND PROPERTY STRINGS ${BACKEND_VALUES})
list(FIND BACKEND_VALUES ${BACKEND} BACKEND_INDEX)

if(${BACKEND_INDEX} EQUAL -1)
    message(WARNING "Backend ${BACKEND} not supported, valid items are: ${BACKEND_VALUES}")
    set(BACKEND "LINUX")
endif()

string(TOUPPER "${BACKEND}" BACKEND)
add_definitions("-DROUTER_BACKEND_${BACKEND}")

set(CMAKE_BUILD_TYPE release)

add_subdirectory(HAL)
add_subdirectory(Router)
