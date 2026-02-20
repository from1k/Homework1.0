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

### Для работы с размерностью файлов необходимы следущие команды:
1. ```du``` (Disk Usage) возвращает размер каталогов и файлов
2. ```sort``` предназначит для задания условия сортировки
3. ```head``` выводит начало файла или потока данных.

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

*Примечание: создаем новую директорию под названием "boost_1_69_0" и извлекаем файлы из архива в неё.*

### Задание 3. Подсчитайте количество файлов в директории ~/boost_1_69_0 не включая вложенные директории. 

**Решение в терминале:** 

```bash 
find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l
``` 
*Примечание: в команде используется pipe "|", который предназначен для группировки команд и передачи вывода одной команды на вход другой.*

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
*Примечание: в команде используется pipe "|", который предназначен для группировки команд и передачи вывода одной команды на вход другой.*

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
*Примечание: \(...\) используется так, чтобы скобки объединяли условия, необходимо "экранировать" скобки. Знак "!" используется как стандартное отрицание (инверсия) условия.*

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

*Для удобства можно добавить:*

```bash 
grep -rl "boost::asio" ~/boost_1_69_0 | less
```

*Можно перенаправить вывод и записать данный результат в файл:*

```bash 
grep -rl "boost::asio" ~/boost_1_69_0 > asio_files.txt
```

*Примечание: ">" используется для перенаправления. Результат команды ```grep``` записывается в файл [asio_files.txt](/asio_files.txt)*

### Задание 8. Скомпилирутйе boost (можно воспользоваться инструкцией [по ссылке](https://codeyarns.com/tech/2017-01-24-how-to-build-boost-on-linux.html).

**Решение в терминале:** 

```bash 
cd ~/boost_1_69_0
~/boost_1_69_0$ ./bootstrap.sh
./b2
```

*Примечание: если на стадии ```~/boost_1_69_0$ ./bootstrap.sh``` терминал выдает ошибку, тогда необходимо проверить наличие компилятора C++ (g++) и дркгих зависимостей*

### Задание 9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию ~/boost-libs.

**Решение в терминале:** 

```bash 
mkdir -p ~/boost-libs
find ~/boost_1_69_0 -type f -name "*.a" -exec mv {} ~/boost-libs \;
``` 

### Задание 10.	Подсчитайте сколько занимает дискового пространства каждый файл в новой директории.

**Решение в терминале:** 

```bash 
du -h ~/boost-libs/*
```

**Вывод в терминале:**

  ```bash
4.0K /home/from1k/boost-libs/libboost_atomic.a
236K /home/from1k/boost-libs/libboost_chrono.a
148K /home/from1k/boost-libs/libboost_container.a
24K /home/from1k/boost-libs/libboost_context.a
332K /home/from1k/boost-libs/libboost_contract.a
152K /home/from1k/boost-libs/libboost_date_time.a
4.0K /home/from1k/boost-libs/libboost_exception.a
232K /home/from1k/boost-libs/libboost_fiber.a
416K /home/from1k/boost-libs/libboost_filesystem.a
848K /home/from1k/boost-libs/libboost_graph.a
172K /home/from1k/boost-libs/libboost_iostreams.a
2.0M /home/from1k/boost-libs/libboost_locale.a
544K /home/from1k/boost-libs/libboost_math_c99.a
448K /home/from1k/boost-libs/libboost_math_c99f.a
464K /home/from1k/boost-libs/libboost_math_c99l.a
2.7M /home/from1k/boost-libs/libboost_math_tr1.a
2.6M /home/from1k/boost-libs/libboost_math_tr1f.a
2.7M /home/from1k/boost-libs/libboost_math_tr1l.a
212K /home/from1k/boost-libs/libboost_prg_exec_monitor.a
1.6M /home/from1k/boost-libs/libboost_program_options.a
80K /home/from1k/boost-libs/libboost_random.a
2.7M /home/from1k/boost-libs/libboost_regex.a
1.2M /home/from1k/boost-libs/libboost_serialization.a
24K /home/from1k/boost-libs/libboost_stacktrace_addr2line.a
20K /home/from1k/boost-libs/libboost_stacktrace_backtrace.a
16K /home/from1k/boost-libs/libboost_stacktrace_basic.a
4.0K /home/from1k/boost-libs/libboost_stacktrace_noop.a
4.0K /home/from1k/boost-libs/libboost_system.a
2.3M /home/from1k/boost-libs/libboost_test_exec_monitor.a
56K /home/from1k/boost-libs/libboost_timer.a
2.3M /home/from1k/boost-libs/libboost_unit_test_framework.a
4.5M /home/from1k/boost-libs/libboost_wave.a
796K /home/from1k/boost-libs/libboost_wserialization.a
  ```

### Задание 11.	Найдите 10 самых "тяжелых" файлов в новой директории.

**Решение в терминале:** 

```bash 
du -h ~/boost-libs/* | sort -hr | head -n 10
```

**Вывод в терминале:**

  ```bash
4.5M /home/from1k/boost-libs/libboost_wave.a
2.7M /home/from1k/boost-libs/libboost_regex.a
2.7M /home/from1k/boost-libs/libboost_math_tr1l.a
2.7M /home/from1k/boost-libs/libboost_math_tr1.a
2.6M /home/from1k/boost-libs/libboost_math_tr1f.a
2.3M /home/from1k/boost-libs/libboost_unit_test_framework.a
2.3M /home/from1k/boost-libs/libboost_test_exec_monitor.a
2.0M /home/from1k/boost-libs/libboost_locale.a
1.6M /home/from1k/boost-libs/libboost_program_options.a
1.2M /home/from1k/boost-libs/libboost_serialization.a
  ```

</details>
