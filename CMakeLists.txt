cmake_minimum_required(VERSION 3.16)
project(superbuild)

include(ExternalProject)

# ConfMMap 组件 - 基础依赖
ExternalProject_Add(ConfMMap
    SOURCE_DIR ${CMAKE_SOURCE_DIR}/../components/ConfMMap
    INSTALL_DIR ${SYSROOT_DIR}
    CMAKE_ARGS
        -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
)

# DataOperation 组件 
ExternalProject_Add(DataOperation
    SOURCE_DIR ${CMAKE_SOURCE_DIR}/../components/Common/DataOperation
    INSTALL_DIR ${SYSROOT_DIR}
    CMAKE_ARGS
        -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
)

ExternalProject_Add(OTA
    SOURCE_DIR ${CMAKE_SOURCE_DIR}/../components/OTA
    DEPENDS ConfMMap DataOperation
    CMAKE_ARGS
        -DCMAKE_PREFIX_PATH=${SYSROOT_DIR}
        -DFXLOG_ROOT=${CMAKE_BINARY_DIR}/sysroot
        -DSYSROOT_DIR=${SYSROOT_DIR}
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
