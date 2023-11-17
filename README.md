#information_security-HW_13-02
## VADIM TSVETKOV

«Защита хоста»

**Задание 1.**

Установим ecryptfs в ВМ под управлением Debian 11:

apt install ecryptfs-utils cryptsetup -y

Добавим пользователя cryptouser:

sudo adduser cryptouser

su - cryptouser

Создадим файлы в домашнем каталоге пользователя /home/cryptouser и зашифруем с помощью eCryptfs:

touch text netology top

Зашифровать получилось только после установки модуля:

![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/1.1.jpg)

Далее:

sudo ecryptfs-migrate-home -u cryptouser

sudo ls -la /home/cryptouser

![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/1.2.jpg)
![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/1.3.jpg)
![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/1.4.jpg)

**Задание 2.**

Установим поддержку luks:
sudo apt install cryptsetup -y

Создадим новый раздел размером 100 МБ с помощью утилиты gparted:

sudo apt install gparted -y
sudo gparted
![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/2.1.jpg)
![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/2.2.jpg)

Зашифруем созданный раздел:

Зададим тип файловой системы - luks2 для раздела /dev/sdb2:
sudo cryptsetup -y -v --type luks2 luksFormat /dev/sdb2
![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/2.3.jpg)

Смонтируем раздел и отформатиркем раздел:

sudo cryptsetup luksOpen /dev/sdb2 luks_disk

ls /dev/mapper/luks_disk

sudo dd if=/dev/zero of=/dev/mapper/luks_disk

sudo mkfs.ext4 /dev/mapper/luks_disk

![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/2.4.jpg)

Монтируем открытый раздел:

mkdir .secret

sudo mount /dev/mapper/luks_disk .secret/

![img](https://github.com/vadimtsvetkov/information_security-HW_13-02/blob/main/2.5.jpg)
