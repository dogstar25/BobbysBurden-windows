cmake_minimum_required(VERSION 3.28)
project(BobbysBurdenWindows LANGUAGES CXX)

# ---------------------------------------------------------
# Compiler setup
# ---------------------------------------------------------
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# ---------------------------------------------------------
# Submodules
# ---------------------------------------------------------
add_subdirectory(MobyDick)
add_subdirectory(BobbysBurden)

# ---------------------------------------------------------
# Game executable
# ---------------------------------------------------------
add_executable(BobbysBurdenGame
    ${CMAKE_CURRENT_SOURCE_DIR}/src/bobbysBurden.cpp
)

target_link_libraries(BobbysBurdenGame
    PRIVATE
        BobbysBurden
        MobyDick
)

# ---------------------------------------------------------
# Visual Studio run configuration
# ---------------------------------------------------------
set_property(TARGET BobbysBurdenGame
    PROPERTY VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}"
)

message(STATUS "✅ Configured BobbysBurdenWindows successfully.")
