# Projects Settings
cmake_minimum_required(VERSION 4.2)
project(sald-breakout)

if(UNIX)
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-rpath='$ORIGIN'")
endif()

add_executable(${PROJECT_NAME})

set_target_properties(${PROJECT_NAME} PROPERTIES DEBUG_POSTFIX "d")

target_sources(${PROJECT_NAME}
    PRIVATE
    src/main.cpp
    src/BallObject.cpp
    src/BreakoutApp.cpp
    src/GameLayer.cpp
    src/GameLevel.cpp
    src/GameObject.cpp
)

add_subdirectory(vendor/sald)

target_include_directories(${PROJECT_NAME} PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src
)

target_link_libraries(${PROJECT_NAME} PRIVATE sald)

install(TARGETS ${PROJECT_NAME}
    DESTINATION ${PROJECT_SOURCE_DIR}/release
)

install(DIRECTORY src/Shaders
    DESTINATION ${PROJECT_SOURCE_DIR}/release
)

install(DIRECTORY src/Textures
    DESTINATION ${PROJECT_SOURCE_DIR}/release
)

install(DIRECTORY src/Levels
    DESTINATION ${PROJECT_SOURCE_DIR}/release
)
