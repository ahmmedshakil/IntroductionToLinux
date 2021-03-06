В этой инструкции создается простой RAID1.
На 1-ом жестком диске у нас система,  2-й и 3-й объединяем в RAID1

Смотрим какие разделы файловой системы у нас уже есть. Убеждаемся, что 2-й и 3-й жесткие диски еще не примонтированы и рейда не создано.

`$ df -h`

Смотрим какие разделы жестких дисков, жесткие диски доступны.

`$ cat /proc/partitions/`

Создаем разделы на новых (2 и 3) дисках.
Для 2-го диска

`$ sudo fdisk /dev/sdb`

p // смотрим, что разделов на нем нет  
n // создаем новый раздел  
p // создаем primary раздел  
1 // первый раздел  
нажимаем Enter  
p // смотрим, что раздел появился  
w // записываем изменения  

Аналогичное проделываем на 3-ем диске

`$ sudo fdisk /dev/sdc`

p // смотрим, что разделов на нем нет  
n // создаем новый раздел  
p // создаем primary раздел  
1 // первый раздел  
нажимаем Enter  
p // смотрим, что раздел появился  
w // записываем изменения  

Смотрим разделы жестких дисков, что добавились.

`$ cat /proc/partitions/`

Создаем RAID1

`$ sudo mdadm -C /dev/md0 -a yes -l 1 -n 2 /dev/sdb1 /dev/sdc1`  
// -C означает create  
// -l 1 оначает уровень RAID, у нас RAID1  
// -n 2 означает количество разделов-участников  

Нажимаем Enter

Смотрим разделы жестких дисков  
`$ cat /proc/partitions/`

Создаем файловую систему на рейде  
`sudo mkfs.ext3 /dev/md0`

Монтируем получившийся рейд md0 в папку /mnt  
`sudo mount /dev/md0 /mnt`

Проверяем, смотрим список смонтированных разделов  
`$ df -h`

Для проверки работы рейда создаем файл file.avi из нулей (10000 блоков по 4096 байт)  
`sudo dd if=/dev/zero of=/mnt/file.avi bs=4096 count=10000`

Переходим в директорию /mnt  
`cd /mnt`

Смотрим на файлы в директории /mnt  
`ls -l`

Источник: https://www.youtube.com/watch?v=NeR95b_w8GI&t=2s

Спасибо Евгению Красникову
