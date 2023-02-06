cmake_minimum_required(VERSION 3.8.2)

project(qtdarkstyle)

# Find includes in the build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Turn on automatic invocation of the MOC, UIC & RCC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

message("This is great : ${AUTOUIC_EXECUTABLE}")

# There may be a way to tell up front if Qt5 is going to be found, but I haven't found
# a foolproof way to do it yet, so settle for the default error message for now.
#if(NOT CMAKE_PREFIX_PATH AND NOT Qt5Widgets_DIR)
#    message(WARNING "CMAKE_PREFIX_PATH is not defined, so find_package may not work. Set the CMAKE_PREFIX_PATH "
#            "environment variable to the install prefix of Qt 5, either on the command line as "
#            "-DCMAKE_PREFIX_PATH=\"path/to/Qt5/lib/cmake\" or with set(CMAKE_PREFIX_PATH path/to/Qt5/lib/cmake)")
#endif(NOT CMAKE_PREFIX_PATH AND NOT Qt5Widgets_DIR)

# Add a compiler flag
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

# Make this a GUI application on Windows
if(WIN32)
  set(CMAKE_WIN32_EXECUTABLE ON)
endif()

# Find the QtWidgets library
find_package(Qt5 REQUIRED COMPONENTS Core Gui Widgets)

set(HEADERS
    DarkStyle.h
    framelesswindow.h
    mainwindow.h
    windowdragger.h
)

set(SRCS
    DarkStyle.cpp
    framelesswindow.cpp
    main.cpp
    mainwindow.cpp
    windowdragger.cpp
)

set(RCS
    darkstyle.qrc
    framelesswindow.qrc
)

set(UI
    framelesswindow.ui
    mainwindow.ui
)

# Tell CMake to create the helloworld executable
add_executable(qtdarkstyle ${SRCS} ${HEADERS} ${UI} ${RCS})

target_include_directories(qtdarkstyle PRIVATE include)
# Add the Qt5 Widgets for linking
target_link_libraries(qtdarkstyle Qt5::Core Qt5::Gui Qt5::Widgets)