# Enovates-Home-Advanced-Charging-Station
Serial connection to the Enovates Home Advanced Charging Station

# Enovates HOMEADVANCED Charger

## **Requirements**:

- Serial port cable + gender changer: for example the “DIGITUS Serial Port Slot Bracket Adapter Cable 10 Pin IDC to D-Sub 9 Female Plug to Connector Flat Ribbon Cable” (pinout assignment: 1-1; 6-2; 2-3; 7-4; 3-5; 8-6; 4-7; 4-7; 9-8; 5-9) and the “DIGITUS D-Sub 9 Gender Changer Adapter Connector 9 Pin Female to Female RS-232 RS-485 TTL Metal Housing”
    
    ### D‑Sub9 (male) ↔ 10‑pin IDC pinout
    
    | **D‑Sub9 Pin** | **IDC Header Wire** |
    | --- | --- |
    | 1 → 1 | D‑Sub pin 1 ↔ IDC pin 1 |
    | 2 → 3 | D‑Sub pin 2 ↔ IDC pin 3 |
    | 3 → 5 | D‑Sub pin 3 ↔ IDC pin 5 |
    | 4 → 7 | D‑Sub pin 4 ↔ IDC pin 7 |
    | 5 → 9 | D‑Sub pin 5 ↔ IDC pin 9 |
    | 6 → 2 | D‑Sub pin 6 ↔ IDC pin 2 |
    | 7 → 4 | D‑Sub pin 7 ↔ IDC pin 4 |
    | 8 → 6 | D‑Sub pin 8 ↔ IDC pin 6 |
    | 9 → 8 | D‑Sub pin 9 ↔ IDC pin 8 |
    
https://www.amazon.com.be/-/en/dp/B006DYQNIK?ref=ppx_yo2ov_dt_b_fed_asin_title



- USB to Serial Adapter (DB9), for example (untested):

https://www.amazon.com.be/-/en/gp/product/B00BBVXWFM/ref=ox_sc_act_title_1?smid=A3Q3FYJVX702M2&th=1


  
- RJ45 erthernet UTP cable to a network with a dhcp server

## **Procedure:**

- Attach the UTP cable to your network and to the charging station, check for the leds to come up.Green = normal rj45 ethernet UTP connection(Red is not required: this is the rj11 Load-Balancing connection)


- Connect the Serial console cable to your pc with the usb serial adapter using a DB9 Female to Female cable (straight!) or a D-Sub 9 Gender Changer Female/Female.

  
- Choose serial port settings 115200 8N1 in your favourite serial software (minicom, putty,…)
- Press ‘Enter’ to connect, the following prompt should appear.

```
Welcome to minicom 2.10

OPTIONS: I18n 
Port /dev/ttyUSB0, 12:37:52 [U]

Press CTRL-A Z for help on special keys

                                        
Password:                               
Login incorrect                         
                                        
charger login: root                     
Password:                               
Last login: Mon Feb  2 20:44:40 +0000 2026 on pts/0 from 10.11.1.254.
root@charger:~#
```

- Run ‘ip a’ to determine the ip address of eth0 (10.11.1.100 in my case):

```
root@charger:~# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether [REDACTED] brd ff:ff:ff:ff:ff:ff
    inet 10.11.1.100/24 brd 10.11.1.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 [REDACTED] scope link 
       valid_lft forever preferred_lft forever
3: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default 
    link/ipip 0.0.0.0 brd 0.0.0.0
4: ip_vti0@NONE: <NOARP> mtu 1364 qdisc noop state DOWN group default 
    link/ipip 0.0.0.0 brd 0.0.0.0
```

- Run the ‘grep admin.web.secured.password /opt/charger/LCCL/etc/lccl.properties’ command to find the web interface admin password

```
root@charger:~# grep admin.web.secured.password /opt/charger/LCCL/etc/lccl.properties
admin.web.secured.password=[REDACTED]
```

- Browse to the ip addres of your charger on port 12800 to go the web interfaceTwo important urls exist: http://10.11.1.100:12800/admin/admin.html] and http://10.11.1.100:12800/user/user.html 
The admin page requires a password, the user page does not.

- Fill in anything you want in the first popup, admin will work fine for example.



- In the following screen the username is admin, and the password is the one you grepped in the [lccl.properties](http://lccl.properties) file.

