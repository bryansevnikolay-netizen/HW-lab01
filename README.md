## Laboratory work I

## Homework

1. Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.
```sh 
$ wget
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
$ wget -o file1.txt https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
// перенаправление результата команды в файл file1.txt
```    

2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0`
```sh    
$ tar
$ tar -xf boost_1_69_0.tar.gz -C ~
```

3. Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.
```sh
$ find, wc
$ find -maxdepth 1 ! -type d | wc -l
// 12
```
    
4. Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.
```sh
$ find, wc
$ find ! -type d | wc -l
// 61191
```
    
5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).
```sh    
$ find, wc
$ find ! -type d -name "*.h" | wc -l
//296
$ find ! -type d -name "*.cpp" | wc -l
// 13774
$ find ! -type d  ! -name "*.cpp" ! -name "*.h" | wc -l
// 13774
``` 

6. Найдите полный путь до файла `any.hpp` внутри библиотеки *boost*.
```sh 
$ find
$ find -name "any.hpp"
/* 
./boost/xpressive/detail/utility/any.hpp
./boost/hana/fwd/any.hpp
./boost/hana/any.hpp
./boost/type_erasure/any.hpp
./boost/any.hpp
./boost/fusion/algorithm/query/any.hpp
./boost/fusion/algorithm/query/detail/any.hpp
./boost/fusion/include/any.hpp
./boost/spirit/home/support/algorithm/any.hpp
./boost/proto/detail/any.hpp
*/
```

7. Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.
```sh
$ grep
$ grep -lr "boost::asio"
$ grep -lr "boost::asio" > file7.txt
// перенаправление результата команды в файл file7.txt
```    

8. Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).
```sh
$ ./bootstrap.sh
$ sudo ./b2 install
$ ./bootstrap.sh &> file8.txt
$ sudo ./b2 install &>> file8.txt
// перенаправление результата команды в файл file8.txt
```

9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.
```sh
$ mkdir, find, cp
$ $ mkdir ~/boost-libs
$ cp `find -name "*.a"` ~/boost-libs
```

10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.
```sh
$ cd, find, -exec {} +
$ cd ~/boost-libs
$ find ! -type d -exec du -h {} +
/*
2.7M	./libboost_regex.a
2.7M	./libboost_math_tr1.a
2.3M	./libboost_unit_test_framework.a
2.3M	./libboost_test_exec_monitor.a
332K	./libboost_contract.a
796K	./libboost_wserialization.a
4.0K	./libboost_atomic.a
80K	./libboost_random.a
212K	./libboost_prg_exec_monitor.a
56K	./libboost_timer.a
24K	./libboost_context.a
4.0K	./libboost_exception.a
2.0M	./libboost_locale.a
148K	./libboost_container.a
2.6M	./libboost_math_tr1f.a
20K	./libboost_stacktrace_backtrace.a
416K	./libboost_filesystem.a
544K	./libboost_math_c99.a
24K	./libboost_stacktrace_addr2line.a
172K	./libboost_iostreams.a
232K	./libboost_fiber.a
4.0K	./libboost_stacktrace_noop.a
464K	./libboost_math_c99l.a
1.2M	./libboost_serialization.a
2.7M	./libboost_math_tr1l.a
16K	./libboost_stacktrace_basic.a
1.6M	./libboost_program_options.a
4.5M	./libboost_wave.a
848K	./libboost_graph.a
236K	./libboost_chrono.a
152K	./libboost_date_time.a
448K	./libboost_math_c99f.a
4.0K	./libboost_system.a
*/
```

11. Найдите *топ10* самых "тяжёлых".
```sh
$ find ! -type d -exec du {} + | sort -rn | head -n 10
/*
4588	./libboost_wave.a
2756	./libboost_regex.a
2732	./libboost_math_tr1.a
2700	./libboost_math_tr1l.a
2648	./libboost_math_tr1f.a
2308	./libboost_test_exec_monitor.a
2288	./libboost_unit_test_framework.a
2044	./libboost_locale.a
1576	./libboost_program_options.a
1200	./libboost_serialization.a
*/
```
