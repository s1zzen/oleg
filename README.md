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

