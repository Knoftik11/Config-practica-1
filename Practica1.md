# Задание 1
![image](https://github.com/user-attachments/assets/3df30e28-8189-4b97-8486-7f60f1dadd75)
```
grep '.*' /etc/passwd | cut -d':' -f1 | sort
```
![image](https://github.com/user-attachments/assets/63e722aa-8073-451f-9ef1-9c03ae91b7f8)


# Задание 2
![image](https://github.com/user-attachments/assets/426740ca-f56d-4cec-9822-b16415717b48)

```
cat /etc/protocols | awk '{print $2, $1}' | sort -nr | head -5
```
![image](https://github.com/user-attachments/assets/0ae6fbd7-6b9f-4516-98ee-9e40b7d28acc)

# Задание 3
![image](https://github.com/user-attachments/assets/dd2fb258-40e6-48a8-8506-9b264f86afbf)

```
nano banner.sh
```
```
#!/bin/bash
 
if [ $# exit 1]; then
        echo "Использование: $0 \"Hello from RTU MIREA!\""
        exit 1
fi
 
text="$1"
text_length=${#text}
border_length=$((text_length + 4))
 
#Вывод верхней границы
echo "+$(printf -- '-%.0s' $(seq 1 $border_length))+"
 
# Вывод текста в баннере
echo "| $text   |"
 
# Вывод нижней границы
echo "+$(printf -- '-%.0s' $(seq 1 $border_length))+"
```
```
chmod +x banner.sh
```
```
./banner.sh "Hello from RTU MIREA!"
```
![image](https://github.com/user-attachments/assets/2e6defda-7070-4d41-aff2-6f6a955b6878)

# Задание 4
![image](https://github.com/user-attachments/assets/fc2d8022-a836-4299-803d-51fde6bdec2b)

```
nano hello.c
```
```
#include <stdio.h>

void hello() {
    printf("Hello, world!\n");
}

int main() {
    hello();
    return 0;
}
```
```
grep -o -E '\b[_a-zA-Z][_a-zA-Z0-9]*\b' hello.c | sort | uniq
```
![image](https://github.com/user-attachments/assets/85e495dc-ee89-4f51-905d-7daecd1124f3)

# Задание 5
![image](https://github.com/user-attachments/assets/537d2c60-8d6a-4507-b30a-4833dceafcc4)

```
nano reg
```
```
#!/bin/bash
 
if [ $# -ne 1 ]; then
        echo "Использование: $0 <команда>"
        exit 1
fi
 
command="$1"
 
if [ -x "$command" ]; then
        echo "Команда $command уже существует и имеет исполняемые права."
        exit 1
fi
 
if [ -f "$command" ]; then
        chmod +x "$command"
        cp "$command" /usr/local/bin/
        echo "Команда $command зарегистрирована и скопирована в /usr/local/bin/"
else
        echo "Команда $command не найдена."
        exit 1
fi
```
```
chmod +x reg
```
```
./reg banner.sh
```
```
cat reg
```
```
./reg banner.sh
```
```
sudo cp banner.sh /usr/local/bin/
```
```
ls -l /usr/local/bin/banner.sh
```
```
banner.sh "Hello from RTU MIREA!"
```
![image](https://github.com/user-attachments/assets/e22edc68-ad3e-4c27-91ac-c9b909cfb327)

# Задание 6
![image](https://github.com/user-attachments/assets/760d1f8e-129b-425e-ae88-e1afd92bbf9e)

```
nano check_comments.sh
```
```
#!/bin/bash
 
if [ $# -ne 1 ]; then
        echo "Использование: $0 <путь_к_каталогу>"
        exit 1
fi
 
directory="$1"
 
# Проверяем, существует ли указанный каталог
if [ ! -d "$directory" ]; then
        echo "Каталог $directory не существует."
        exit 1
fi
 
# Проверяем наличие комментария в первой строке файла
check_comment() {
        local file="$1"
        local extension="${file##*.}"  # Получаем расширение файла
 
        # Если расширение файла соответствует .c, .js или .py
        if [[ "$extension" == "c" || "$extension" == "js" || "$extension" == "py" ]]; then
                # Считываем первую строку файла и проверяем, начинается ли она с комментария
                first_line=$(head -n 1 "$file")
                if [[ "$first_line" =~ ^[[:space:]]*\/\/.* || "$first_line" =~ ^[[:space:]]*#.* ]]; then
                        echo "Файл $file содержит комментарий в первой строке."
                else
                        echo "Файл $file не содержит комментария в первой строке."
                fi
        fi
}
```
```
chmod +x check_comments.sh
```
```
pwd
```
```
ls -R
```
```
./check_comments.sh .
```
```
cat check_comments.sh
```
![image](https://github.com/user-attachments/assets/73a0c1d8-ad0d-4c5f-b6ad-2b5c640abafc)
![image](https://github.com/user-attachments/assets/b9fcccfc-07a8-47d1-992e-57b83b65a736)

# Задание 7 
![image](https://github.com/user-attachments/assets/d5c89e47-e9c1-4940-ba6d-d14357ad7a16)

```
nano find_duplicates.sh
```
```
#!/bin/bash

if [ $# -ne 1 ]; then
  echo "Использование: $0 <путь_к_каталогу>"
  exit 1
fi

directory="$1"

# Поиск дубликатов с использованием md5sum
find "$directory" -type f -print0 | xargs -0 md5sum | sort | uniq -d -w 32 | sed -r 's/^[0-9a-f]*( )//' | while read -r duplicate; do
  echo "Дубликат: $duplicate"
done
```
```
chmod +x find_duplicates.sh
```
```
./find_duplicates.sh /root
```
![image](https://github.com/user-attachments/assets/bb24ec8e-bc94-4ee2-af50-f1342db2f81f)
![image](https://github.com/user-attachments/assets/859e4811-8bc5-4ae7-b955-87345bb80780)
![image](https://github.com/user-attachments/assets/1bb5f1eb-572e-4998-92a5-8c5bb8df1b28)

# Задание 8 
![image](https://github.com/user-attachments/assets/c3ef3d6f-d046-4bac-807e-956420a96e09)

```
nano archive_files.sh
 ```
```
#!/bin/bash

if [ $# -ne 2 ]; then
  echo "Использование: $0 <расширение_файлов> <имя_архива>"
  exit 1
fi

extension="$1"
archive_name="$2"

# Поиск файлов с заданным расширением в текущем каталоге
files=$(find . -type f -name "*.$extension")

# Проверка наличия файлов
if [ -z "$files" ]; then
  echo "Файлов с расширением .$extension не найдено."
  exit 1
fi

# Архивация файлов
tar -czvf "$archive_name.tar.gz" $files

echo "Файлы с расширением .$extension были архивированы в $archive_name.tar.gz"
```
```
./archive_files.sh txt myarchive
```
```
tar -tzvf myarchive.tar.gz
```
```
ls -l
```
```
ls -ld .
```
![image](https://github.com/user-attachments/assets/9cbe49c9-deef-4e4d-b16f-69824c33171b)
![image](https://github.com/user-attachments/assets/3a130833-b7ab-43aa-a297-184ecc415843)

# Задание 9
![image](https://github.com/user-attachments/assets/85c1ae8c-1049-4011-a5b7-9f2bc4c0d843)

```
nano replace_spaces.sh
```
```
#!/bin/bash

if [ $# -ne 2 ]; then
  echo "Использование: $0 <входной_файл> <выходной_файл>"
  exit 1
fi

input_file="$1"
output_file="$2"

# Проверка существования входного файла
if [ ! -f "$input_file" ]; then
  echo "Входной файл $input_file не существует."
  exit 1
fi

# Замена последовательностей из 4 пробелов на символ табуляции и запись в выходной файл
sed 's/    /\t/g' "$input_file" > "$output_file"

echo "Замена завершена. Результат сохранен в $output_file."
```
```
chmod +x replace_spaces.sh
```
```
echo "This is a test file with    four spaces." > input.txt
```
```
cat input.txt
```
```
./replace_spaces.sh input.txt output.txt
```
```
cat output.txt
```
```
od -c output.txt
```
![image](https://github.com/user-attachments/assets/659523f5-d048-40b8-b6bb-36fcb0632586)

# Задание 10
![image](https://github.com/user-attachments/assets/0b760768-de19-4317-8272-17a1b03e512a)

```
nano find_empty_files.sh
```
```
#!/bin/bash

if [ $# -ne 1 ]; then
  echo "Использование: $0 <директория>"
  exit 1
fi

directory="$1"

# Проверка существования указанной директории
if [ ! -d "$directory" ]; then
  echo "Директория $directory не существует."
  exit 1
fi

# Поиск пустых текстовых файлов
find "$directory" -type f -empty -exec file {} \; | grep "empty" | cut -d: -f1
```
```
find /home/testdir -maxdepth 1 -type f -size 0c
```
![image](https://github.com/user-attachments/assets/570e80d6-e5d4-4966-9ee2-790fa7010563)
![image](https://github.com/user-attachments/assets/00f6e7e9-3103-40c2-9da8-5252006b12a7)
