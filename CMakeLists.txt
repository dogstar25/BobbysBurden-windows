cmake_minimum_required(VERSION 3.28)

# Allow older vcpkg packages (like jsoncpp) to configure under modern CMake
if(NOT DEFINED CMAKE_POLICY_VERSION_MINIMUM)
    set(CMAKE_POLICY_VERSION_MINIMUM 3.5)
endif()

if(POLICY CMP0126)
    cmake_policy(SET CMP0126 NEW)
endif()

project(BobbysBurdenWindows LANGUAGES CXX)

# ---------------------------------------------------------
# Compiler setup
# ---------------------------------------------------------
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Define the asset path for the engine and all games that use it and we have to use cache so
# that the MobyDick CMAKELists.txt can see this variable
set(GAME_WORKING_DIR "BobbysBurden" CACHE STRING "Relative path to game assets" FORCE)

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



message(STATUS "Configured BobbysBurdenWindows successfully.")
