"# elvis_wiki" 

# Создаем wifi точку доступа и получаем доступ к устройству через статический IP 

Целевая система:
v24.11.1 for Orange Pi PC + running Armbian Linux 6.6.62-current-sunxi

## 1. Отключаем dns на systemd-resolved

> nano /etc/systemd/resolved.conf
```
DNSStubListener=no
```

## 2. Задаем статический IP для wlan1 
> nano /etc/netplan/00-default-use-network-manager.yaml
```
network:
  version: 2
  renderer: networkd
  ethernets:
    wlan1:
      dhcp4: false
      dhcp6: false
      addresses:
        - 192.168.100.70/24
```
> netplan apply

## 3. Настраиваем DNS сервер dnsmasq
> nano /etc/dnsmasq.conf
```
interface=wlan1
dhcp-range=192.168.100.64,192.168.100.200,12h
domain=wlan     # Local wireless DNS domain
dhcp-host=11:22:33:44:55:66,fred,192.168.100.70,45
dhcp-host=11:22:33:44:55:66,ignore
dhcp-authoritative
```
> systemctl restart dnsmasq

## 4. Настраиваем точку доступа hostapd
> nano /etc/hostapd/hostapd.conf
```
interface=wlan1
driver=nl80211
hw_mode=g
channel=9
ssid=mywifi
auth_algs=1
macaddr_acl=0
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP CCMP
wpa_passphrase=12345678
```
> systemctl restart hostapd

## Ссылки
1. https://habr.com/ru/articles/188274/
2. https://innerlife.io/ru/home-router-nas-dc-orange-pi-plus-wifi-hostapd/
3. https://winitpro.ru/index.php/2022/08/17/wi-fi-tochka-dostupa-na-linux/
4. https://dh-organization.gitbook.io/droneshub-rover-kontakt/rabota-s-orange-pi/nastroika-staticheskogo-ip-adresa-na-orange-pi-5-5-plus
5. https://www.dmosk.ru/miniinstruktions.php?mini=network-netplan


