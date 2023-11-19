cmake_minimum_required(VERSION 3.16)

project(ND-Notes VERSION 0.0.1 LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 REQUIRED COMPONENTS Widgets)
qt_standard_project_setup()

set(PROJECT_SOURCES
  main.cpp
  mainwindow.cpp
  mainwindow.h
  mainwindow.ui
)

qt_add_executable(ND-Notes
  MANUAL_FINALIZATION
  ${PROJECT_SOURCES}
)

target_link_libraries(ND-Notes PRIVATE Qt6::Widgets)

set_target_properties(ND-Notes PROPERTIES
    ${BUNDLE_ID_OPTION}
    WIN32_EXECUTABLE ON
)

include(GNUInstallDirs)
install(TARGETS ND-Notes
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET ND-Notes
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})

qt_finalize_executable(ND-Notes)
