cmake_minimum_required(VERSION 3.28)

project(DungeonForge
    VERSION 0.1.0
    LANGUAGES CXX
)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

include(FetchContent)

FetchContent_Declare(
    SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 3.1.0
    GIT_SHALLOW ON
    EXCLUDE_FROM_ALL
    SYSTEM
)

FetchContent_MakeAvailable(SFML)

add_executable(
    DungeonForge
    src/main.cpp
)

target_compile_features(
    DungeonForge
    PRIVATE cxx_std_20
)

set_target_properties(
    DungeonForge
    PROPERTIES
        CXX_EXTENSIONS OFF
)

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
  target_compile_options(
        DungeonForge
        PRIVATE
            -Wall
            -Wextra
            -Wpedantic
    )
elseif(MSVC)
  target_compile_options(
        DungeonForge
        PRIVATE /W4
    )
endif()

target_link_libraries(
    DungeonForge
    PRIVATE SFML::Graphics
)

set_property(
    DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    PROPERTY VS_STARTUP_PROJECT DungeonForge
)
