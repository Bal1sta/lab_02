# Указываем минимальную версию CMake
cmake_minimum_required(VERSION 3.10)

# Указываем имя проекта и его версию
project(IFilterProject VERSION 0.1.0)

# Указываем стандарт C++
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Указываем директорию для заголовочных файлов
include_directories(include)

# Находим библиотеки Boost
find_package(Boost REQUIRED COMPONENTS filesystem system)  # Укажите нужные компоненты

if (Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})  # Добавляем директории заголовков Boost
endif()

# Находим библиотеку OpenMPI
find_package(OpenMPI REQUIRED)

# Указываем исходные файлы
file(GLOB SOURCES "src/*.cpp")

# Создаем исполняемый файл
add_executable(IFilterProject ${SOURCES})

# Связываем библиотеки с исполняемым файлом
target_link_libraries(IFilterProject PRIVATE ${Boost_LIBRARIES} OpenMPI::OpenMPI)

# Добавляем тесты (если используете Google Test или аналогичные)
enable_testing()
add_subdirectory(tests)  # Предполагаем, что тесты находятся в подкаталоге tests

# Устанавливаем правила для создания пакета
include(CPack)