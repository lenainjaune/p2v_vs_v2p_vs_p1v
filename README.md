# p2v_vs_v2p_vs_p1v

Attention : p1v est le nom que je donne à cette technique et cette désignation n'est pas officielle alors que p2v l'est
# p1v
p1v = physical integered to virtual = solution pratique pour gérer un support physique directement dans une machine virtuelle (attention : il est impératif d'utiliser un identifiant unique - voir dessous).

Je m'en sert dans les cas suivants :
* gérer un support depuis la même machine physique ou dockée par USB (ex : migration lnj-ubu64 -> golu)
* gérer un support importé par NBD depuis une autre machine (physique ou virtuelle) qui exporte ses supports par NBD (voir [mon github](https://github.com/lenainjaune/nbd_remote_disk))

## Trouver un identifiant unique d'un disque physique
Il est impératif de renseigner le nom du support par un identifiant unique /dev/disk/by-id ... et NON /dev/sdh, qui pourrait référer à un autre support ultérieurement.

```sh
user@host:~# find /dev -type l -exec ls -al {} \; | grep sdc$
lrwxrwxrwx 1 root root 9 mars 31 18:08 /dev/disk/by-path/pci-0000:00:1f.2-ata-3 -> ../../sdc
lrwxrwxrwx 1 root root 9 mars 31 18:08 /dev/disk/by-id/wwn-0x50014ee2b54b2579 -> ../../sdc
lrwxrwxrwx 1 root root 9 mars 31 18:08 /dev/disk/by-id/ata-WDC_WD5000AAKX-08U6AA0_WD-WCC2ER3N9DL0 -> ../../sdc
lrwxrwxrwx 1 root root 6 mars 31 18:08 /dev/block/8:32 -> ../sdc
```

# p2v
Physical to Virtual = solution pratique pour transformer en ligne une machine physique en machine virtuelle avec des outils tel VMWare

Le point essentiel est que l'opération peut se faire à chaud (système en ligne), ce qui m'a permis de migrer une machine physique défaillante en VM alors qu'elle était encore utilisée (expérience professionnelle).

Aussi pour Linux j'ai expérimenté la sauvegarde d'un système en ligne (voir [mon github](https://github.com/lenainjaune/backup_system_online) et #438 où j'ai cloné sur un vHD externe le système Debian d'un utilisateur alors qu'il l'utilisait pour pouvoir faire des tests sur ce vHD)
# v2p
Virtual to Physical = est l'inverse de la p2v (on transforme une machine virtuelle en machine physique
