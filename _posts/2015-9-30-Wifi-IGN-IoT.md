---
layout: post
title: WIFI IGNSDK-IoT
---

![edimax-ew-7811un-150mbps-wireless-ieee80211b-g-n-nano-usb-adapter](https://cloud.githubusercontent.com/assets/4461503/8298796/306dffba-1998-11e5-957f-16cf5751d3b0.jpg)


(1) cek dengan perintah

~~~bash
root@iotign ~ # dmesg
~~~

apabila usb wifi bisa dikenali akan ada keterangan seperti dibawah ini

~~~bash
[ 4404.222079] usb 1-1.4: Product: 802.11n WLAN Adapter
[ 4404.227219] usb 1-1.4: Manufacturer: Realtek
[ 4404.231601] usb 1-1.4: SerialNumber: 00e04c000001
~~~

(2) kemudian cek juga dengan perintah

~~~bash
root@iotign ~ # lsmod
~~~

untuk mengetahui driver bisa digunakan atau tidak apabila driver dikenali akan muncul keterangan seperti dibawah ini

~~~bash
Module                  Size  Used by
8192cu                528365  0 
uio_pdrv_genirq         2958  0 
uio                     8119  1 uio_pdrv_genirq
ipv6                  333976  24 
~~~

(3) cek menggunakan perintah 

~~~bash
root@iotign ~ # ip addr
~~~

apabila ethercard wifi sudah terbaca akan muncul tulisan

~~~bash
4: wlan0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
~~~

(4) aktifkan dengan perintah 

~~~bash
root@iotign ~ # ifconfig wlan0 up
~~~
(5) ketik perintah

~~~bash
root@iotign ~ # iwlist wlan0 scan
~~~  

untuk melakukan scanning Access Point Wifi yang tersedia, apabila ada akan muncul keterangan seperti dibawah

~~~bash
wlan0     Scan completed :
        
          Cell 01 - Address: 00:0C:43:C0:B6:CE
                    ESSID:"malware!!"
                    Protocol:IEEE 802.11bg
                    Mode:Master
                    Frequency:2.437 GHz (Channel 6)
                    Encryption key:on
                    Bit Rates:54 Mb/s
                    Extra:rsn_ie=30140100000fac020100000fac020100000fac020000
                    IE: IEEE 802.11i/WPA2 Version 1
                        Group Cipher : TKIP
                        Pairwise Ciphers (1) : TKIP
                        Authentication Suites (1) : PSK
                    IE: Unknown: DD9D0050F204104A0001101044000102103B000103104700102880288028801880A880000C43C0B6CE1021001852616C696E6B20546563686E6F6C6F67792C20436F72702E1023001C52616C696E6B20576972656C6573732041636365737320506F696E74102400065254323836301042000831323334353637381054000800060050F20400011011000952616C696E6B415053100800020084103C000101
                    Quality=48/100  Signal level=100/100  
~~~

(6) ketik 
~~~bash 
nano /etc/wpa_supplicant/wpa_supplicant.conf
~~~

kemudian tambahkan tulisan dibawah dibagian palah bawah konfigurasi
~~~bash
network={
    ssid="NAMA SSID ACCESS POINT"
    psk="PASSWORD"
}
~~~

(7)setelah diedit restart perangkat jaringan dengan

~~~bash
root@igniot# ifdown wlan0
~~~
~~~bash
root@igniot# ifup wlan0
~~~

(8)reboot
