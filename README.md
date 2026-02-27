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
$ wget -O boost_1_69_0.tar.gz https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
``` 

**Вывод в терминале:**

  ```bash
Resolving sourceforge.net (sourceforge.net)... 104.18.12.149, 104.18.13.149, 2606:4700::6812:c95, ...
Connecting to sourceforge.net (sourceforge.net)|104.18.12.149|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/ [following]
--2026-02-26 18:49:34--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/
Reusing existing connection to sourceforge.net:443.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/download [following]
--2026-02-26 18:49:34--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/download
Reusing existing connection to sourceforge.net:443.
HTTP request sent, awaiting response... 302 Found
Location: https://downloads.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?ts=gAAAAABpoGuPxWHIALKG4S8yHCNMVZfDlZpA_CAzapLvQKD5iXMRgPWrMxst_XvqqdhSQ1KmO8WTmHMm9xWNE05OBl32gbHk3Q%3D%3D&use_mirror=altushost-swe&r= [following]
--2026-02-26 18:49:35--  https://downloads.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?ts=gAAAAABpoGuPxWHIALKG4S8yHCNMVZfDlZpA_CAzapLvQKD5iXMRgPWrMxst_XvqqdhSQ1KmO8WTmHMm9xWNE05OBl32gbHk3Q%3D%3D&use_mirror=altushost-swe&r=
Resolving downloads.sourceforge.net (downloads.sourceforge.net)... 104.18.13.149, 104.18.12.149, 2606:4700::6812:c95, ...
Connecting to downloads.sourceforge.net (downloads.sourceforge.net)|104.18.13.149|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://altushost-swe.dl.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?viasf=1 [following]
--2026-02-26 18:49:35--  https://altushost-swe.dl.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?viasf=1 
Resolving altushost-swe.dl.sourceforge.net (altushost-swe.dl.sourceforge.net)... 79.142.76.130
Connecting to altushost-swe.dl.sourceforge.net (altushost-swe.dl.sourceforge.net)|79.142.76.130|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 111710205 (107M) [application/x-gzip]
Saving to: ‘boost_1_69_0.tar.gz’

2026-02-26 18:49:51 (7.10 MB/s) - ‘boost_1_69_0.tar.gz’ saved [111710205/111710205]
  ```

### Задание 2. Разархивируйте скаченный файл в директорию ~/boost_1_69_0. 

**Решение в терминале:** 

```bash 
$ mkdir -p ~/boost_1_69_0
$ tar -xzvf boost_1_69_0.tar.gz -C ~/
``` 

*Примечание: создаем новую директорию под названием "boost_1_69_0" и извлекаем файлы из архива в неё.*

### Задание 3. Подсчитайте количество файлов в директории ~/boost_1_69_0 не включая вложенные директории. 

**Решение в терминале:** 

```bash 
$ find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l
``` 
*Примечание: в команде используется pipe "|", который предназначен для группировки команд и передачи вывода одной команды на вход другой.*

**Вывод в терминале:**

  ```bash
$ find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l 
12
  ```

### Задание 4. Подсчитайте количество файлов в директории ~/boost_1_69_0 включая вложенные директории. 

**Решение в терминале:** 

```bash 
$ find ~/boost_1_69_0 -type f | wc -l
``` 
*Примечание: в команде используется pipe "|", который предназначен для группировки команд и передачи вывода одной команды на вход другой.*

**Вывод в терминале:**

  ```bash
$ find ~/boost_1_69_0 -type f | wc -l 
61191
  ```

### Задание 5. Подсчитайте количество заголовочных файлов, файлов с расширением .cpp, сколько остальных файлов (не заголовочных и не .cpp).

**Решение в терминале:** 

```bash 
$ find ~/boost_1_69_0 -type f \( -name "*.hpp" -o -name "*.h" \) | wc -l
$ find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
$ find ~/boost_1_69_0 -type f ! -name "*.hpp" ! -name "*.h" ! -name "*.cpp" | wc -l
``` 
*Примечание: \(...\) используется так, чтобы скобки объединяли условия, необходимо "экранировать" скобки. Знак "!" используется как стандартное отрицание (инверсия) условия.*

**Вывод в терминале:**

  ```bash
$ find ~/boost_1_69_0 -type f \( -name "*.hpp" -o -name "*.h" \) | wc -l
15208
$ find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
13774
$ from1k@from1k-VirtualBox:~$ find ~/boost_1_69_0 -type f ! -name "*.hpp" ! -name "*.h" ! -name "*.cpp" | wc -l
32209
  ```

### Задание 6. Найдите полный путь до файла any.hpp внутри библиотеки boost.

**Решение в терминале:** 

```bash 
$ find ~/boost_1_69_0 -type f -name "any.hpp"
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
$ grep -rl "boost::asio" ~/boost_1_69_0
```

*Для удобства можно добавить:*

```bash 
$ grep -rl "boost::asio" ~/boost_1_69_0 | less
```

*Можно перенаправить вывод и записать данный результат в файл:*

```bash 
$ grep -rl "boost::asio" ~/boost_1_69_0 > asio_files.txt
```

*Примечание: ">" используется для перенаправления. Результат команды ```grep``` записывается в файл [asio_files.txt](#file-asio_files-txt)*

### Задание 8. Скомпилирутйе boost (можно воспользоваться инструкцией [по ссылке](https://codeyarns.com/tech/2017-01-24-how-to-build-boost-on-linux.html).

**Решение в терминале:** 

```bash 
$ cd ~/boost_1_69_0
$ ./bootstrap.sh
```

**Вывод(1):** 

```bash 
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Unicode/ICU support for Boost.Regex?... not found.
Backing up existing Boost.Build configuration in project-config.jam.1
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:

    ./b2
    
To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help
     
   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html
     
   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html
```

```bash 
$ ./b2
```

**Вывод(2):** 

Вывод данного действия достаточно огромен, чтобы не вставлять его сюда целиком. Однако в случае возникновения проблем с компиляцией (или желания ознакомиться с данным выводом) для ознакомления прикрепляю файл [build.txt](#file-output-txt)
*Описание: в файле расположен вывод процесса компиляции, в связи с проблемами совместимости некоторых файлов я был вынужден обратиться к более новой версии boost C++ (1-90-0), компиляция считается успешной, за исключением отдельного компонента MPI. Если Boost.MPI не сильно нужен, то можно явно отключить MPI и Python, чтобы не видеть данной ошибки. При необходимости данного компонента достаточно установить MPI:*

```bash
$ sudo apt install libopenmpi-dev openmpi-bin
$ mkdir -p ~/.config/boost-build
$ nano ~/.config/boost-build/user-config.jam
```
*Добавим строку ```using mpi : /usr/bin/mpic++ ;```. Для указания пути можно использовать ```which mpic++```. Сохраняем.* 
*Затем достаточно пересобрать Boost.*

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
