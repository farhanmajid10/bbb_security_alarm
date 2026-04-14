cmake_minimum_required(VERSION 3.16)
project(bbb_security_alarm VERSION 1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(lib/GPIO)
add_subdirectory(lib/Buzzer)
add_subdirectory(lib/I2CDevice)
add_subdirectory(lib/MPU6050)
add_subdirectory(lib/PIR)
add_subdirectory(lib/PWM)
add_subdirectory(lib/SSD1306)

add_executable(security_alarm src/main.cpp)
target_link_libraries(security_alarm
    GPIO PWM Buzzer MPU6050 PIR SSD1306 I2CDevice
)

add_executable(test_pir test/test_pir.cpp)
target_link_libraries(test_pir GPIO PIR)

add_executable(test_mpu6050 test/test_mpu6050.cpp)
target_link_libraries(test_mpu6050 I2CDevice MPU6050)

add_executable(test_oled test/test_oled.cpp)
target_link_libraries(test_oled I2CDevice SSD1306)

add_executable(test_buzzer test/test_buzzer.cpp)
target_link_libraries(test_buzzer GPIO PWM Buzzer)