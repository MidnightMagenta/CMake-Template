cmake_minimum_required(VERSION 3.10)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set(ProjectName "project_name")
set(Subsystem "CONSOLE")

project("${ProjectName}" VERSION 0.1)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc")

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

add_dependencies("${ProjectName}" q_start_clock)