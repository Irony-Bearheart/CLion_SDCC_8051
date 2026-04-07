cmake_minimum_required(VERSION 3.20)
project(SDCC_8051 C)

add_executable(${PROJECT_NAME}
        main.c
)

target_include_directories(${PROJECT_NAME} PRIVATE inc)

target_compile_options(${PROJECT_NAME} PRIVATE --opt-code-size)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
        COMMAND packihx ${PROJECT_NAME}.ihx > ${PROJECT_NAME}.hex
        WORKING_DIRECTORY $<TARGET_FILE_DIR:${PROJECT_NAME}>
        COMMENT "Converting IHX to HEX"
)
