# oleg

### Базовый код

```bash
#!/bin/bash
date +%Y.%m.%d-%H.%M
find . -type f -name "*.txt" | while read filename; do
    basename "$filename"
done
ps aux | awk 'NR <= 6 { print }'
new_dir="new_directory"
mkdir $new_dir
new_file="new_file.txt"
echo "new file" > $new_file
cat $new_file | awk '{ print $1 }'
rm $new_file
rmdir $new_dir»
```

### Пометки

####  1. #!/bin/bash
В первой строке скрипта стоит **shebang**
Этот элемент сценария сообщает оболочке, в которой будет выполняться этот скрипт, какую подоболочку следует выполнить для запуска этого сценария. shebang всегда начинается с #!. А далее следует имя подоболочки, которая должна выполнить скрипт.
В папке  bin/ находится программа(интерпритатор скрипта) bash. 

#### 2. date +%Y.%m.%d-%H.%M
Отображает текущую дату и время в формате ГГГГ.ММ.ДД-ЧЧ.ММ.
выполняет команду date. после идет указание формата вывода, где:
  `+` - начало ввода формата
  `%Y %m %d %H %M` - вставил год, месяц, день, часы, и минуты в заданном порядке и с заданными разделителями.

#### 3. Цикл
```bash
find . -type f -name "*.txt" | while read filename; do
    basename "$filename"
done
```
##### 3.1 find
Команда `find . -type f -name "*.txt"` выводит все файлы(с путем) с .txt на конце в текущей папке и во всех папках внутри этой папки.
пример вывода команды:
```
./myNewDir/text4.txt
./text3.txt
./text2.txt
./text1.txt
```
##### 3.2 | while
Далее идет `| wile read filename;`, где `|` означает, что вывод команды find передается в цикл while,
`read` означает, что цикл считывает все строчки, которые печатает `find`, и каждую строчку заварачивает в переменную `filename`.
Дальше для каждого выведеного пути к файлу применяется код(тело цикла, между `do` и `done`).

##### 3.3 basename
Имя файла передается через переменную, ее вызов обозначается `$filename`.
Получая имя фала с путем возвращает чистое имя файла(`./myNewDir/text4.txt` -> `text4.txt`).

#### 4. Список процессов
```bash
ps aux | awk 'NR <= 6 { print }'
```

##### 4.1 ps aux
ps - для отображения информации о запущенных процессах в системе, печатает как `top`, только печатает.

Опции команды ps:

**a**: показывает процессы для всех пользователей, включая те, которые не принадлежат текущему пользователю;

**u**: отображает подробную информацию о каждом процессе, включая пользователя, который владеет процессом;

**x**: включает процессы, которые не имеют управляющего терминала.(демоны(процессы в фоновом выполнении(как службы в виндоус)))

Пример вывода:
  ps:
```bash
    PID TTY          TIME CMD
   1605 pts/4    00:00:00 sudo
   1606 pts/4    00:00:00 su
   1607 pts/4    00:00:00 bash
   7041 pts/4    00:00:00 ps
```
  ps aux:
  ```bash
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0  21720 12032 ?        Ss   12:49   0:00 /sbin/init
root          46  0.0  0.0  50436 13896 ?        Ss   12:49   0:00 /usr/lib/syst
systemd+      93  0.0  0.0  18980  7424 ?        Ss   12:49   0:00 /usr/lib/syst
systemd+     210  0.0  0.0  21576 12416 ?        Ss   12:49   0:00 /usr/lib/syst
root         215  0.0  0.0  18028  7808 ?        S<s  12:49   0:00 /usr/lib/syst
root         216  0.0  0.0   3808  2048 ?        Ss   12:49   0:00 /usr/sbin/cro
message+     217  0.0  0.0   9536  4736 ?        Ss   12:49   0:00 @dbus-daemon
root         219  0.0  0.0  29396 17920 ?        Ss   12:49   0:00 /usr/bin/pyth
root         231  0.0  0.0   2732  1536 pts/0    Ss+  12:49   0:00 /sbin/agetty
root         232  0.0  0.0   6808  4352 pts/1    Ss   12:49   0:00 /bin/login -p
root         233  0.0  0.0   2732  1664 pts/2    Ss+  12:49   0:00 /sbin/agetty
root         240  0.0  0.0  12020  7552 ?        Ss   12:49   0:00 sshd: /usr/sb
syslog       264  0.0  0.0 222508  4224 ?        Ssl  12:49   0:00 /usr/sbin/rsy
root         418  0.0  0.0  42848  4624 ?        Ss   12:49   0:00 /usr/lib/post
postfix      420  0.0  0.0  43332  7680 ?        S    12:49   0:00 qmgr -l -t un
root         424  0.0  0.0   2716  1280 ?        Ss   12:49   0:00 runsvdir -P /
root         432  0.0  0.0   2564  1280 ?        Ss   12:49   0:00 runsv sidekiq
root         433  0.0  0.0   2564  1280 ?        Ss   12:49   0:00 runsv gitlab-
root         434  0.0  0.0   2564  1280 ?        Ss   12:49   0:00 runsv gitlab-
root         435  0.0  0.0   2564  1280 ?        Ss   12:49   0:00 runsv postgre
root         436  0.0  0.0   2564  1280 ?        Ss   12:49   0:00 runsv gitlab-
root         437  0.0  0.0   2564  1280 ?        Ss   12:49   0:00 runsv puma
```
##### 4.2 awk
```bash
awk 'NR <= 6 { print }'
```
Команда awk - один из самых мощных инструментов для обработки и фильтрации текста, доступный даже для людей никак не связных с программированием. Это не просто утилита, а целый язык разработанный для обработки и извлечения данных. В этой статье мы разберемся как пользоваться awk.

NR - общее количество строк в обрабатываемом тексте;
по итогу программа awk получает на вход вывод команды ps и выводит первые шесть строк.

Подробнее про awk [тут](https://losst.pro/ispolzovanie-awk-v-linux#google_vignette).

По итогу будет выведено пять записей + шапка таблицы:
```bash
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0  21720 12032 ?        Ss   12:49   0:00 /sbin/init
root          46  0.0  0.0  50436 13896 ?        Ss   12:49   0:00 /usr/lib/systemd/systemd-journald
systemd+      93  0.0  0.0  18980  7424 ?        Ss   12:49   0:00 /usr/lib/systemd/systemd-networkd
systemd+     210  0.0  0.0  21576 12416 ?        Ss   12:49   0:00 /usr/lib/systemd/systemd-resolved
root         215  0.0  0.0  18028  7808 ?        S<s  12:49   0:00 /usr/lib/systemd/systemd-logind
```

#### 5. Операции с файлами
Создает переменную `new_dir` и присваивает ей значение "new_directory".
```bash
new_dir="new_directory"
```
Создает новую директорию с именем, указанным в переменной `new_dir`.
```bash
mkdir $new_dir
```
Создает переменную `new_file` и присваивает ей значение "new_file.txt".
```bash
new_file="new_file.txt"
```
Создает новый файл с именем, указанным в переменной `new_file`, и записывает в него строку "new file".
```bash
echo "new file" > $new_file
```
Считывает содержимое файла `new_file` и с помощью `awk` выводит только первый столбец каждой строки.
```bash
cat $new_file | awk '{ print $1 }'
```
Удаляет файл, указанный в переменной `new_file`.
```bash
rm $new_file
```
Удаляет директорию, указанную в переменной `new_dir`.
```bash
rmdir $new_dir
```

### Дополнение
Для обращения к переменной, нужно поставить знак $ перед ее названием:
```bash
root@gitlab:~# new_dir="new_directory"
root@gitlab:~# echo $new_dir
new_directory
```

