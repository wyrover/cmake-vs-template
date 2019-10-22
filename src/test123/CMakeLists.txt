# 源码根路径
set(INCROOT ${PROJECT_SOURCE_DIR}/include/SFML/Audio)
set(SRCROOT ${PROJECT_SOURCE_DIR}/src/test123)

# 源码路径
set(SRC
    ${SRCROOT}/abc.h
    ${SRCROOT}/abc.cpp    
)
# 筛选器
source_group("模块" FILES ${SRC})

# 预编译头
# if(MSVC)	
# 	set (PRECOMPILED_SOURCE ${SRC})
# 	list(REMOVE_ITEM PRECOMPILED_SOURCE ${SRCROOT}/stdafx.cpp)
# 	set (PRECOMPILED_BINARY ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.pch)
# 	set_source_files_properties (${PRECOMPILED_SOURCE} PROPERTIES COMPILE_FLAGS "/Yu\"stdafx.h\" /Fp\"${PRECOMPILED_BINARY}\"" OBJECT_DEPENDS "${PRECOMPILED_BINARY}")
# 	set_source_files_properties (${SRCROOT}/stdafx.cpp PROPERTIES COMPILE_FLAGS "/Yc\"stdafx.h\" /Fp\"${PRECOMPILED_BINARY}\"" OBJECT_OUTPUTS "${PRECOMPILED_BINARY}")
# endif (MSVC)


if(WIN32)
    #TODO: Is XML_STATIC only required with Windows? What does it do?
    add_definitions(-DXML_STATIC)
else()
    add_definitions(-DXML_NS -DXML_DTD -DHAVE_EXPAT_CONFIG_H)
endif()




# vs 工程名
# 静态库
add_library(test123 ${SRC})

# 动态库
add_library(test1234 SHARED ${SRC})

# 特定 vs 工程头文件路径
target_include_directories(test123 PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/ppppppp")
target_link_libraries(test123 PRIVATE ws2_32)



