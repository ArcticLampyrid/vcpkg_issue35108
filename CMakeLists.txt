cmake_minimum_required(VERSION 3.28)
project(test VERSION 0.1)
find_package(Qt6 REQUIRED COMPONENTS Quick)
qt_standard_project_setup()
qt_add_executable(test
    "include/main.h"
    "src/main.cpp")
target_include_directories(test PRIVATE "include")
qt_add_qml_module(test 
    URI test 
    RESOURCE_PREFIX / 
    VERSION 1.0 
    QML_FILES
        "qml/app.qml")
if(VCPKG_TARGET_TRIPLET MATCHES "-windows-static$")
    set_property(TARGET test PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()
target_link_libraries(test PRIVATE Qt6::Quick)