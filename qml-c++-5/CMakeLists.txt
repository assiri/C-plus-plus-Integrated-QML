cmake_minimum_required(VERSION 3.16)
project(qml-c++-5 VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(QT NAMES Qt5 Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui Quick)

qt_standard_project_setup()

qt_add_executable(qml-c++-5 WIN32 MACOSX_BUNDLE
    machine.cpp machine.h
    main.cpp
)
target_compile_definitions(qml-c++-5 PRIVATE
    QT_DEPRECATED_WARNINGS
)

target_link_libraries(qml-c++-5 PRIVATE
    Qt::Core
    Qt::Gui
    Qt::Quick
)


# Resources:
set(qml_resource_files
    "main.qml"
)

qt_add_resources(qml-c++-5 "qml"
    PREFIX
        "/"
    FILES
        ${qml_resource_files}
)

install(TARGETS qml-c++-5
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET qml-c++-5
    FILENAME_VARIABLE deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
