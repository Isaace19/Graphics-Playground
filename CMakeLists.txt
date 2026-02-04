cmake_minimum_required(VERSION 3.5...3.10)
project(MagnumPhysics)

set(CMAKE_CXX_STANDARD 23)

# Add the modules directory to CMAKE_MODULE_PATH so find_package can locate the libraries
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/magnum/modules/" ${CMAKE_MODULE_PATH})

# build corrade first
add_subdirectory(corrade EXCLUDE_FROM_ALL)

# build magnum
set(MAGNUM_WITH_SDL2APPLICATION ON CACHE BOOL "" FORCE)
add_subdirectory(magnum EXCLUDE_FROM_ALL)

# Find the required Magnum packages after adding the subdirectories
find_package(Magnum REQUIRED
    GL
    Sdl2Application
    Primitives
    MeshTools
    Shaders
    SceneGraph
    Trade
)

# Build TriangleExample from src/
add_executable(TriangleExample src/TriangleExample.cpp)
target_link_libraries(TriangleExample PRIVATE
    Corrade::Main
    Magnum::Application
    Magnum::GL
    Magnum::Magnum
    Magnum::MeshTools
    Magnum::Primitives
    Magnum::SceneGraph
    Magnum::Shaders
    Magnum::Trade
)

# Build individual files in GraphicsTest/ (only if they have main function)
# add_executable(basic GraphicsTest/dev/basic.cpp)
# target_link_libraries(basic PRIVATE
#     Corrade::Main
#     Magnum::Application
#     Magnum::GL
#     Magnum::Magnum
#     Magnum::MeshTools
#     Magnum::Primitives
#     Magnum::SceneGraph
#     Magnum::Shaders
#     Magnum::Trade
# )