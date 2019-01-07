cmake_minimum_required(VERSION 3.10)

project(UriParser VERSION 0.9.1 LANGUAGES C)

file(GLOB INTERFACE_FILES
        RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" CONFIGURE_DEPENDS
        "include/uriparser/*.h")
set_source_files_properties("${INTERFACE_FILES}" PROPERY PUBLIC_HEADER 1)

file(GLOB SOURCE_FILES
        RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" CONFIGURE_DEPENDS
        "src/*.[c|h]")

add_library(uriparser ${INTERFACE_FILES} ${SOURCE_FILES})
target_include_directories(uriparser PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>)
target_include_directories(uriparser PUBLIC $<INSTALL_INTERFACE:include>)

install(TARGETS uriparser
        EXPORT uriparser
        LIBRARY
            DESTINATION lib
        ARCHIVE
           DESTINATION lib
        PUBLIC_HEADER
            DESTINATION include/uriparser
        )

install(EXPORT uriparser
        DESTINATION lib/cmake/uriparser
        NAMESPACE UriParser::
        )

