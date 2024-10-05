cmake_minimum_required(VERSION 3.10)  # Устанавливаем минимальную версию CMake, необходимую для сборки проекта

project(ip_filter)  # Название проекта

# Установка C++ стандарта
set(CMAKE_CXX_STANDARD 17)  # Устанавливаем стандарт языка C++ на 17
set(CMAKE_CXX_STANDARD_REQUIRED True)  # Обязательное использование указанного стандарта

# Добавляем исполняемый файл
add_executable(ip_filter ip_filter.cpp)  # Создаем исполняемый файл 'ip_filter' из исходного файла 'ip_filter.cpp'

# Устанавливаем путь для тестов
add_executable(test_ip_filter test_ip_filter.cpp)  # Создаем исполняемый файл 'test_ip_filter' из исходного файла 'test_ip_filter.cpp'

# Подключаем библиотеку Boost для тестирования
find_package(Boost 1.65 REQUIRED COMPONENTS unit_test_framework)  # Находим библиотеку Boost версии 1.65 и требуем компонент 'unit_test_framework'

if(Boost_FOUND)  # Проверяем, найдена ли библиотека Boost
    include_directories(${Boost_INCLUDE_DIRS})  # Добавляем директории с заголовочными файлами Boost в проект
    target_link_libraries(test_ip_filter ${Boost_LIBRARIES})  # Линкуем библиотеку Boost с исполняемым файлом тестов
endif()  # Конец проверки наличия библиотеки Boost

enable_testing()  # Включаем поддержку тестирования в CMake

# Добавляем тест
add_test(NAME IPFilterTests COMMAND test_ip_filter)  # Добавляем тест с именем 'IPFilterTests', который запускает исполняемый файл 'test_ip_filter'