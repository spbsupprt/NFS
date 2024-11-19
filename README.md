# NFS
Основная часть: 
- vagrant up должен поднимать 2 настроенных виртуальных машины (сервер NFS и клиента) без дополнительных ручных действий; (опционально.)
- на сервере NFS должна быть подготовлена и экспортирована директория; 
- в экспортированной директории должна быть поддиректория с именем upload с правами на запись в неё; 
- экспортированная директория должна автоматически монтироваться на клиенте при старте виртуальной машины (systemd, autofs или fstab — любым способом);
- монтирование и работа NFS на клиенте должна быть организована с использованием NFSv3.

# Выполнение:

 - 2 настроенных виртуальных машины (сервер NFS и клиента) без дополнительных ручных действий

![image](https://github.com/user-attachments/assets/b66264fb-27bb-4f8c-9a19-2a8bced3fd25)


- на сервере NFS должна быть подготовлена и экспортирована директория

На сервере:

mkdir -p /srv/share/upload 

chown -R nobody:nogroup /srv/share 

chmod 0777 /srv/share/upload 

echo "/srv/share 192.168.122.12/24(rw,sync,root_squash)" >> /etc/exports

![image](https://github.com/user-attachments/assets/eeb30e2e-e392-401f-838b-e5bbd499b938)


На клеинте:

echo "192.168.122.11:/srv/share/ /mnt nfs vers=3,noauto,x-systemd.automount 0 0
" >> /etc/fstab

systemctl daemon-reload

![image](https://github.com/user-attachments/assets/c205f7c8-965b-4eac-a1b2-2ec7cc768855)

Файл 111.txt в расшарен по сети.

- монтирование и работа NFS на клиенте должна быть организована с использованием NFSv3

![image](https://github.com/user-attachments/assets/76129170-c62d-49cc-ad4c-1eb617b8f257)
