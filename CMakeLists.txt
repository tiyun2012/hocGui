cmake_minimum_required(VERSION 3.0.0)
project(IMgui_A VERSION 0.1.0)

include(CTest)
enable_testing()
message( STATUS "----------CMAKE_SOURCE_DIR is-----------: ${CMAKE_SOURCE_DIR}")
set(IMGUI_SRC imgui.cpp
              imgui_draw.cpp 
              imgui_widgets.cpp
              imgui_tables.cpp
              imgui_impl_opengl3.cpp
              imgui_impl_glfw.cpp 
    )

# Add the GLFW include directory
include_directories(${CMAKE_SOURCE_DIR})
include_directories(${CMAKE_SOURCE_DIR}/GLFW)
# Add the OpenGL include directory
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIR})
message(STATUS "---------------GL DIR---------------------:: ${OPENGL_INCLUDE_DIR}")
# Add the GLFW library
add_library(glfw STATIC IMPORTED)
set_target_properties(glfw PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/lib-vc2022/glfw3.lib)

add_executable(IMgui_A imgui_demo.cpp ${IMGUI_SRC})
target_link_libraries(IMgui_A glfw opengl32)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
