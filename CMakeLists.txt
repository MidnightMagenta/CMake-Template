cmake_minimum_required(VERSION 3.10)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set(ProjectName "project_name")
set(Subsystem "CONSOLE")

project("${ProjectName}" VERSION 0.1)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc")
find_package(OpenGL REQUIRED)

add_custom_target(q_start_clock ALL
    COMMENT "Starting console clock"
    COMMAND "${PROJECT_SOURCE_DIR}/console_clock/bin/run.bat"
    WORKING_DIRECTORY "${PROJECT_SOURCE_DIR}/console_clock/bin"
)

#app executable
add_executable("${ProjectName}"
        #src files
        src/main.cpp
        #header files
)

if(Subsystem STREQUAL "CONSOLE")
    set_target_properties("${ProjectName}" PROPERTIES LINK_FLAGS /SUBSYSTEM:CONSOLE)
    target_compile_definitions("${ProjectName}" PRIVATE SUBSYSTEM_CONSOLE)
elseif (Subsystem STREQUAL "WINDOWS")
    set_target_properties("${ProjectName}" PROPERTIES LINK_FLAGS /SUBSYSTEM:WINDOWS)
    target_compile_definitions("${ProjectName}" PRIVATE SUBSYSTEM_WINDOWS)
endif ()

add_dependencies("${ProjectName}" q_start_clock)