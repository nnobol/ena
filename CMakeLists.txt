cmake_minimum_required(VERSION 3.20)

project(ena LANGUAGES C)

include(FetchContent)

FetchContent_Declare(
    utf8proc
    GIT_REPOSITORY https://github.com/JuliaStrings/utf8proc.git
    GIT_TAG        v2.10.0
)

FetchContent_MakeAvailable(utf8proc)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

add_executable(ena src/main.c)

target_link_libraries(ena PRIVATE utf8proc)

if (CMAKE_C_COMPILER_ID MATCHES "Clang|GNU")
    target_compile_options(ena PRIVATE -Wall -Wextra -pedantic -Werror)
elseif (CMAKE_C_COMPILER_ID STREQUAL "MSVC")
    target_compile_options(ena PRIVATE /W4 /permissive- /WX)
endif()