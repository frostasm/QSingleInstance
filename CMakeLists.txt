cmake_minimum_required(VERSION 3.14)
project(QSingleInstance VERSION 1.2.2 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED 17)

set(MAIN_PROJECT OFF)
if (CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
    set(MAIN_PROJECT ON)
endif()

add_subdirectory(QSingleInstance)

if (${MAIN_PROJECT})
    # not implemented
    # add_subdirectory(CoreTest)
    # add_subdirectory(GuiTest)
    # add_subdirectory(WidgetTest)
endif()


