# Минимальная версия CMake
cmake_minimum_required(VERSION 3.10)

# Название проекта
project(ip_filter)

# Включаем стандарт C++17
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Добавляем исполняемый файл
add_executable(ip_filter ip_filter.cpp)

# Добавляем файлы для тестов, если нужны
# add_executable(test_ip_filter test_main.cpp ip_filter.cpp)
