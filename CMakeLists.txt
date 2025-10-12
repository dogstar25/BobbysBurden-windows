cmake_minimum_required(VERSION 3.28)
project(BobbysBurdenGame VERSION 0.1.0 LANGUAGES CXX)

# Ensure we use the same C++ version as the engine
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Enable multi-processor builds
add_compile_options($<$<CXX_COMPILER_ID:MSVC>:/MP>)

# Link against vcpkg via MobyDick's toolchain setup
set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/MobyDick/vcpkg_installed/vcpkg.cmake" CACHE STRING "VCPKG toolchain file")

# Include submodules
add_subdirectory(MobyDick)
add_subdirectory(BobbysBurden)

# Create executable
add_executable(BobbysBurdenGame
    src/main.cpp
)

# Link libraries
target_link_libraries(BobbysBurdenGame
    PRIVATE
        MobyDick
        BobbysBurden
)

# Include directories for headers
target_include_directories(BobbysBurdenGame
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/MobyDick/src
        ${CMAKE_CURRENT_SOURCE_DIR}/BobbysBurden/src
)
