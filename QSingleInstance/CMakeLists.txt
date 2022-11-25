cmake_minimum_required(VERSION 3.14)

project(qsingleinstance VERSION 1.2.2 LANGUAGES CXX)

option(DISABLE_COMPILER_WARNINGS "Disable compiler warnings" OFF)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core Network)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Network)

add_library(${PROJECT_NAME} STATIC
    clientinstance.cpp
    clientinstance.h
    QSingleInstance
    qsingleinstance.cpp
    qsingleinstance.h
    qsingleinstance_p.cpp
    qsingleinstance_p.h
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    Qt${QT_VERSION_MAJOR}::Core
    Qt${QT_VERSION_MAJOR}::Network
)

set_target_properties(${PROJECT_NAME} PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
 )

target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
add_library(qsingleinstance::static ALIAS qsingleinstance)

if (DISABLE_COMPILER_WARNINGS)
    if ( CMAKE_COMPILER_IS_GNUCXX )
        target_compile_options(${PROJECT_NAME} PRIVATE -w)
    endif()
    if ( MSVC )
        target_compile_options(${PROJECT_NAME} PRIVATE /w)
    endif()
endif()

