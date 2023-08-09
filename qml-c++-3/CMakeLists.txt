cmake_minimum_required(VERSION 3.16)
project(qml-c++-3 VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(QT NAMES Qt5 Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui Quick)

qt_standard_project_setup()

qt_add_executable(qml-c++-3 WIN32 MACOSX_BUNDLE
    main.cpp
    test.cpp test.h
)
target_compile_definitions(qml-c++-3 PRIVATE
    QT_DEPRECATED_WARNINGS
)

target_link_libraries(qml-c++-3 PRIVATE
    Qt::Core
    Qt::Gui
    Qt::Quick
)


# Resources:
set(qml_resource_files
    "main.qml"
)

qt_add_resources(qml-c++-3 "qml"
    PREFIX
        "/"
    FILES
        ${qml_resource_files}
)

install(TARGETS qml-c++-3
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET qml-c++-3
    FILENAME_VARIABLE deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
