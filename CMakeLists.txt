cmake_minimum_required(VERSION 3.10)

project(GL-LAB VERSION 1.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

file(GLOB PROJECT_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/Source/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/Source/*.c"
)
file(GLOB PROJECT_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/Source/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/Source/*.hpp"
)

file(GLOB GLAD_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/Source/ThirdParty/glad/src/*.c"
)
file(GLOB GLAD_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/Source/ThirdParty/glad/include/glad/*.h"
)

set(SRC_FILES ${PROJECT_SRC} ${GLAD_SRC})
set(HEADER_FILES ${PROJECT_HEADERS} ${GLAD_HEADERS})

set (GLFW_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Source/ThirdParty/glfw-3.4)
set (GLM_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Source/ThirdParty/glm-0.9.3.2)
set (GLAD_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Source/ThirdParty/glad)

# 为源代码文件设置源组，以便在 IDE 中按目录显示
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/Source FILES ${SRC_FILES} ${HEADER_FILES})

add_executable(${PROJECT_NAME} ${SRC_FILES} ${HEADER_FILES})

target_include_directories(${PROJECT_NAME} PRIVATE
    ${GLM_SOURCE_DIR}
    ${GLAD_SOURCE_DIR}/include
    ${GLFW_SOURCE_DIR}/include
)

# 关键：链接 GLFW 库（glfw 是 GLFW 静态库的目标名）
target_link_libraries(${PROJECT_NAME} PRIVATE glfw)

add_subdirectory(Source/ThirdParty/glfw-3.4)