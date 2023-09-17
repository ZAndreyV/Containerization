# Механизмы пространства имен.
## Изоляция на уровне файловой системы - утилита chroot
1. Создадаем директорию testfolder
```mkdir ~/testfolder```
2. Cоздадаем директорию bin
```mkdir ~/testfolder/bin```
3. Копируем исполняемый файл  в bin
```cp /bin/bash ~/testfolder/bin/```
4. утилита ldd  Производит вывод списка используемых приложением библиотек
```ldd /bin/bash```
5. Создадим директории и добавим файлы
```mkdir lib lib64```
```cp /lib/x86_64-linux-gnu/libtinfo.so.6 lib/```
```cp /lib/x86_64-linux-gnu/libc.so.6 lib/```
```cp /lib64/ld-linux-x86-64.so.2 lib64/```
6.  Запустим chroot
```sudo chroot ~/testfolder```
7. Добаим утилиту ls
```ldd /bin/ls```
8. Добавим файлы
```cp /bin/ls bin/```
```cp /lib/x86_64-linux-gnu/libselinux.so.1 lib/```
```cp /lib/x86_64-linux-gnu/libc.so.6 lib/```
```cp /lib/x86_64-linux-gnu/libpcre2-8.so.0 lib/```
```cp /lib64/ld-linux-x86-64.so.2 lib64/```
9. Запустим chroot и проверим ls
```sudo chroot ~/testfolder```
```ls -la```

## Изоляция на сетевом уровне.
1. Создадим пространство имен с помощью команды ip netns add
```sudo ip netns add test1ns```
2. Запустим оболочку bash в этом пространстве имен
```sudo ip netns exec test1ns bash```
3. Выполнив команду ``ip a`` можно убидиться, что сетевая изоляция прошла успешно

## Изоляция на уровне процессов и сетевом уровне.
1. Используем изоляцию на уровне сети и процессов
```sudo unshare --net --pid --fork --mount-proc /bin/bash```
2. Чтобы проверить изоляцию сети и процесов воспользуемся командами:
```ip a```
```ps aux```