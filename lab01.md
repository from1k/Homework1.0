# Homework 1
## Теоретическая часть 
<details>
  
<summary> Нажмите, чтобы раскрыть </summary>  
  
### wget
- Предназначен для скачивания файлов по URL, в данной работе используется ключ -O, который задает имя сохраняемого файла.
### tar
- Предназначен для работы с архивами (tar.gz), имеет ключи:
1. ```-x``` извлечение файлов из архива.
2. ```-z``` для сжатия применяется утилита gzip
3. ```-v``` выводит список обработанных файлов
4. ```-f, --file=ARCHIVE``` в качестве имени файла архива использует ARCHIVE
5. ```-C``` используется для указания директории распаковки
### find
- Предназначен для различного вида поиска.
1. ```-type f``` используется для поиска только файлов
2. ```-maxdepth``` используется для ограничения глубины поиска (количество перемещений)
3. ```-name``` используется для поиска по названию
### wc (word count)
- ```wc -l``` используется для подсчета строк
### grep
- Предназначен для поиска по содержимому.
1. ```-r``` предназначен для рекурсивного поиска
2. ```-l``` выводит только имена файлов

  </details>
  
## Основная часть
<details>
  
<summary> Нажмите, чтобы раскрыть </summary>  

### Задание 1. Скачайте библиотеку Boost C++ с помощью утилиты wget. 
- Ссылка для скачивания: [https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz](https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz)

**Решение в терминале:** 

```bash 
wget -O boost_1_69_0.tar.gz https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
``` 

**Вывод в терминале:**

  ```bash
boost_1_69_0.tar.gz      100%[===============================>] 106.53M  6.06MB/s    in 76s     

2026-02-20 16:05:31 (1.40 MB/s) - ‘boost_1_69_0.tar.gz’ saved [111710205/111710205]
  ```

### Задание 2. Разархивируйте скаченный файл в директорию ~/boost_1_69_0. 

**Решение в терминале:** 

```bash 
mkdir -p ~/boost_1_69_0
tar -xzvf boost_1_69_0.tar.gz -C ~/
``` 

*Пояснение: создаем новую директорию под названием "boost_1_69_0" и извлекаем файлы из архива в неё.*

### Задание 3. Подсчитайте количество файлов в директории ~/boost_1_69_0 не включая вложенные директории. 

**Решение в терминале:** 

```bash 
find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l
``` 
*Пояснение: в команде используется pipe "|", который предназначен для группировки команд и передачи вывода одной команды на вход другой.*

**Вывод в терминале:**

  ```bash
find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l 
12
  ```

### Задание 4. Подсчитайте количество файлов в директории ~/boost_1_69_0 включая вложенные директории. 

**Решение в терминале:** 

```bash 
find ~/boost_1_69_0 -type f | wc -l
``` 
*Пояснение: в команде используется pipe "|", который предназначен для группировки команд и передачи вывода одной команды на вход другой.*

**Вывод в терминале:**

  ```bash
find ~/boost_1_69_0 -type f | wc -l 
61191
  ```

### Задание 5. Подсчитайте количество заголовочных файлов, файлов с расширением .cpp, сколько остальных файлов (не заголовочных и не .cpp).

**Решение в терминале:** 

```bash 
find ~/boost_1_69_0 -type f \( -name "*.hpp" -o -name "*.h" \) | wc -l
find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
find ~/boost_1_69_0 -type f ! -name "*.hpp" ! -name "*.h" ! -name "*.cpp" | wc -l
``` 
*Пояснение: \(...\) используется так, чтобы скобки объединяли условия, необходимо "экранировать" скобки. Знак "!" используется как стандартное отрицание (инверсия) условия.*

**Вывод в терминале:**

  ```bash
find ~/boost_1_69_0 -type f \( -name "*.hpp" -o -name "*.h" \) | wc -l
15208
find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
13774
from1k@from1k-VirtualBox:~$ find ~/boost_1_69_0 -type f ! -name "*.hpp" ! -name "*.h" ! -name "*.cpp" | wc -l
32209
  ```

### Задание 6. Найдите полный путь до файла any.hpp внутри библиотеки boost.

**Решение в терминале:** 

```bash 
find ~/boost_1_69_0 -type f -name "any.hpp"
``` 

**Вывод в терминале:**

  ```bash
/home/from1k/boost_1_69_0/boost/type_erasure/any.hpp
/home/from1k/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
/home/from1k/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
/home/from1k/boost_1_69_0/boost/fusion/include/any.hpp
/home/from1k/boost_1_69_0/boost/fusion/algorithm/query/any.hpp
/home/from1k/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
/home/from1k/boost_1_69_0/boost/any.hpp
/home/from1k/boost_1_69_0/boost/hana/any.hpp
/home/from1k/boost_1_69_0/boost/hana/fwd/any.hpp
/home/from1k/boost_1_69_0/boost/proto/detail/any.hpp
  ```

### Задание 7. Выведите в консоль все файлы, где упоминается последовательность *boost::asio*.

**Решение в терминале:** 

*Если нужно конкретно вывести все файлы в консоль:*

```bash 
grep -rl "boost::asio" ~/boost_1_69_0
```

*Можно перенаправить вывод и записать данный результат в файл:*

```bash 
grep -rl "boost::asio" ~/boost_1_69_0 > asio_files.txt
```

*Пояснение: ">" используется для перенаправления. Результат команды ```grep``` записывается в файл asio_files.txt*

**Вывод в терминале:**

  ```bash
find ~/boost_1_69_0 -type f \( -name "*.hpp" -o -name "*.h" \) | wc -l
15208
find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
13774
from1k@from1k-VirtualBox:~$ find ~/boost_1_69_0 -type f ! -name "*.hpp" ! -name "*.h" ! -name "*.cpp" | wc -l
32209
  ```

</details>
