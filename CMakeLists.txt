cmake_minimum_required(VERSION 3.0.0)

# cmake 工程名，不影响 vs 工程名
project(hello VERSION 0.1.0)


if(CMAKE_CONFIGURATION_TYPES)
set(CMAKE_CONFIGURATION_TYPES Debug Release)
endif()

# 编译库输出路径
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# cmake 附加模块
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# 设置 cmake 搜索头文件路径
set(CMAKE_INCLUDE_PATH ${CMAKE_INCLUDE_PATH} "${PROJECT_SOURCE_DIR}/include")

# 设置 cmake 搜索库路径
set(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} "${PROJECT_SOURCE_DIR}/lib")



# 通用的 include 路径
include_directories( "${CMAKE_CURRENT_SOURCE_DIR}/123" "${CMAKE_CURRENT_SOURCE_DIR}/456" )

if(MSVC)
    foreach(flag
            CMAKE_CXX_FLAGS CMAKE_CXX_FLAGS_DEBUG CMAKE_CXX_FLAGS_RELEASE
            CMAKE_CXX_FLAGS_MINSIZEREL CMAKE_CXX_FLAGS_RELWITHDEBINFO)
        if(${flag} MATCHES "/MD")
            string(REGEX REPLACE "/MD" "/MT" ${flag} "${${flag}}")
        endif()
    endforeach()

    # 预定义宏
    add_definitions(-D_CRT_SECURE_NO_DEPRECATE -D_SCL_SECURE_NO_WARNINGS)
endif()


add_subdirectory(src/hello123)
add_subdirectory(src/test123)










