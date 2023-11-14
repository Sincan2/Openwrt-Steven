# Openwrt-Steven
OpenWRT SDCARD MikroTik RouterBOARD 750Gr3

Cara Mount system Ke SDCARD

<sup>
opkg update
opkg install kmod-sdhci-mt7620
opkg install block-mount kmod-fs-ext4 e2fsprogs parted
parted -s /dev/mmcblk0 -- mklabel gpt mkpart extroot 2048s -2048s

DEVICE="$(block info | sed -n -e '/MOUNT="\S*\/overlay"/s/:\s.*$//p')"
uci -q delete fstab.rwm
uci set fstab.rwm="mount"
uci set fstab.rwm.device="${DEVICE}"
uci set fstab.rwm.target="/rwm"
uci commit fstab

block info
</sup>

![image](https://github.com/Sincan2/Openwrt-Steven/assets/6367413/3db4c656-0bc7-4797-86f8-0bfdb0645589)

<sup>
DEVICE="$(block info | sed -n -e '/MOUNT="\S*\/overlay"/s/:\s.*$//p')"
uci -q delete fstab.rwm
uci set fstab.rwm="mount"
uci set fstab.rwm.device="${DEVICE}"
uci set fstab.rwm.target="/rwm"
uci commit fstab

DEVICE="/dev/mmcblk0p1"
mkfs.ext4 -L extroot ${DEVICE}
</sup>

![image](https://github.com/Sincan2/Openwrt-Steven/assets/6367413/962c1387-f0ea-458c-848a-6ceecbc8651c)

<sup>
eval $(block info ${DEVICE} | grep -o -e 'UUID="\S*"')
eval $(block info | grep -o -e 'MOUNT="\S*/overlay"')
uci -q delete fstab.extroot
uci set fstab.extroot="mount"
uci set fstab.extroot.uuid="${UUID}"
uci set fstab.extroot.target="${MOUNT}"
uci commit fstab

mount ${DEVICE} /mnt
tar -C ${MOUNT} -cvf - . | tar -C /mnt -xf -
reboot
</sup>

![image](https://github.com/Sincan2/Openwrt-Steven/assets/6367413/964c3cb9-62bd-421c-969c-67d231fa0254)



Rokok Sek Ojo Lali Qe3


