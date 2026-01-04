cmake_minimum_required(VERSION 3.16)
project(superbuild)

include(ExternalProject)

# Logging 组件 - 基础依赖
ExternalProject_Add(logging
    SOURCE_DIR ${CMAKE_SOURCE_DIR}/../components/logging
    INSTALL_DIR ${CMAKE_BINARY_DIR}/sysroot
    CMAKE_ARGS
        -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
)

# Example 工程 - 依赖 logging，需要先编译和安装 logging（不安装 example）
ExternalProject_Add(example
    SOURCE_DIR ${CMAKE_SOURCE_DIR}/../components/example
    DEPENDS logging
    CMAKE_ARGS
        -DCMAKE_PREFIX_PATH=${CMAKE_BINARY_DIR}/sysroot
        -DFXLOG_ROOT=${CMAKE_BINARY_DIR}/sysroot
    INSTALL_COMMAND ""
)

# Qt 工程示例（如果使用 CMake）：
# ExternalProject_Add(qt_app
#     SOURCE_DIR ${CMAKE_SOURCE_DIR}/../components/qt_app
#     DEPENDS logging
#     CMAKE_ARGS
#         -DCMAKE_PREFIX_PATH=${CMAKE_BINARY_DIR}/sysroot
#         -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
# )
# 详细说明请参考 QT_EXAMPLE.md
