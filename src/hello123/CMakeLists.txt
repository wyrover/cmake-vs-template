# 源码根路径
set(INCROOT ${PROJECT_SOURCE_DIR}/include/SFML/Audio)
set(SRCROOT ${PROJECT_SOURCE_DIR}/src/hello123)



IF(NOT CMAKE_BUILD_TYPE)
    SET(CMAKE_BUILD_TYPE "Release")
ENDIF(NOT CMAKE_BUILD_TYPE)

message(${CMAKE_BUILD_TYPE})

if( CMAKE_BUILD_TYPE MATCHES "Debug")	
	set( DEBUG_BUILD TRUE)
	add_definitions(
		-DDEBUG
    )
    set(SRC
        ${SRCROOT}/stdafx.h
        ${SRCROOT}/stdafx.cpp    
        ${SRCROOT}/main.cpp
    )
elseif(CMAKE_BUILD_TYPE MATCHES "Release")
    # 源码路径
    set(SRC
        ${SRCROOT}/stdafx.h
        ${SRCROOT}/stdafx.cpp
        ${SRCROOT}/targetver.h
        ${SRCROOT}/main.cpp
    )
    # 筛选器
    source_group("模块" FILES ${SRC})
endif()







# 预编译头
if(MSVC)	
	set (PRECOMPILED_SOURCE ${SRC})
	list(REMOVE_ITEM PRECOMPILED_SOURCE ${SRCROOT}/stdafx.cpp)
	set (PRECOMPILED_BINARY ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.pch)
	set_source_files_properties (${PRECOMPILED_SOURCE} PROPERTIES COMPILE_FLAGS "/Yu\"stdafx.h\" /Fp\"${PRECOMPILED_BINARY}\"" OBJECT_DEPENDS "${PRECOMPILED_BINARY}")
	set_source_files_properties (${SRCROOT}/stdafx.cpp PROPERTIES COMPILE_FLAGS "/Yc\"stdafx.h\" /Fp\"${PRECOMPILED_BINARY}\"" OBJECT_OUTPUTS "${PRECOMPILED_BINARY}")
endif (MSVC)


if(WIN32)
    #TODO: Is XML_STATIC only required with Windows? What does it do?
    add_definitions(-DXML_STATIC -DXML_NS -DXML_DTD -DHAVE_EXPAT_CONFIG_H)
else()
    add_definitions(-DXML_NS -DXML_DTD -DHAVE_EXPAT_CONFIG_H)
endif()

# vs 工程名
add_executable(hello123 ${SRC})


# 特定 vs 工程头文件路径
target_include_directories(hello123 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(hello123 PRIVATE ws2_32)