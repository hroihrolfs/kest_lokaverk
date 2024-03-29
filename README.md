# kest_lokaverk

1. a) setja hostname og domainname. við breytum /etc/hostname file til þess að breyta hostname-inu. sama hjá client1 og 2.
  command: sudo vi /etc/hostname
![1  etc_hostname file til að breyta hostname](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/919ae632-2eda-4dd4-b0b6-6a12033177e3)
![1 hostname](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/ed40626c-3f73-488f-ab38-d5a0f9044b69)

   b) breyta domainname með resolvconf bæta við /etc/resolvconf/resolv.conf.d/head og bæta við domain ddp.is.
   næst er update-að /etc/resolv.conf með sudo resolv.conf -u.
   og að lokum breyta hosts file og bæta við domnname línunni:
   /etc/hosts
   ![1 domainname-hostsfile](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/a8354ca7-0804-40b5-a3c9-501db8bd43af)


-- -------------------------
2. Static ip á server1. Ég notaði sudo vi /etc/netplan til þess að slökkva á dhcp og setja static ip:
![2 static_ip](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/5008f979-9d87-4804-b561-e6d4b4ce1dad)
bætti við dns server í skref 4.

-- -------------------------

3. dhcp server confguration
   Byrja á því að downloada isc-dhcpd með command: sudo apt install isc-dhcp-server.
   næst var breytt í file /etc/dhcp/dhcpd.conf og bætti þessu við:
   
![3  dhcp server conf file](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/3bcd07f9-b4fc-4533-8d4b-310a72445702)

næst þurfti að breyta dhcp í client1 í yes með /etc/netplan og þá virkaði það.

![3 client1 dhcp virkar](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/cae8e5c6-78a5-4846-b341-e1376ee76192)

sama í client2 með því að breyta sudo vi /etc/sysconfig/network-scripts/ifcfg-ens33 og bæta við dhcp: yes

![3 client3 dhcp virkar](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/eae173a3-0072-41e4-a736-dc27e5a053f1)

sýna virkni:


-- -------------------------

4. installa og config a dns server on server1.

   Byrja á því að installa bind 9 með: sudo apt install bind9

   næst þarf að fara í /etc/bind/named.conf.local og bæta við "zone".
   ![4  dns zone ](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/fa03e28a-8a47-49ac-9604-f8dc21a12eed)

   svo var búið til file db.ddp.is og bætt við client1 og client2:
   ![4  dns bind conf](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/247ae06e-573c-462e-8a20-b2756e894801)

   þá þurfti bara að restarta með sudo systemctl restart bind9 til að það klárast.

   seinasta var að breyta netplan til þess að bæta við dns server.
   ![4  dns netplan](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/065a659c-0c3d-40c9-b44e-122f02720b91)

   þá var þetta komið
   ![4  dns virkar](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/c7a5a420-41c1-4c4a-9827-6e65b20607f1)

-- -------------------------

5. create users byrja á að búa til directory með: mkdir scripts
   næst var að búa til script með: sudo vi create_users.sh og bæta þessu við:
   ![5  useradd script](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/ea9be938-0b28-4fa6-84bc-b96333bce58e)

   svo þurfti að nota chmod +x create_users.sh.
   búa til csv skrá með öllum users sem heitir users.csv.

-- -------------------------

6. sleppti 6.

-- -------------------------

7. Weekly backups: byrja á að búa til script sem fer í gegnum öll home-dir til þess að taka backup af hverju og einu:
   ![7 backupscripts](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/30039e73-5ba9-429b-a23b-b7fe73bcdbc8)

   svo þurfti að breyta permission í excecutable með sudo chmod +x backup.sh.

   að lokum þurfit að breyta crontab file með crontab -e og bæta við:
   ![7 crontabfile nytt](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/43072d63-8701-40fe-acc3-4127e6ae5863)


   hérna er dæmi um að backup.sh virkar
   ![7  eftir að keyra backup sh](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/e6fb27cb-92b2-4d26-b861-94204dd6c5d3)

-- -----------------------------

8. install and config ntp: byrja á að update-a server1 og installa ntp með sudo apt install ntp.

  næst þarf að fara í /etc/ntp.conf og bæta við restrict (sést á mynd): 
  ![8  server ntpconf](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/90a9effa-86ef-4926-a409-52c03f3ca580)

  svo þurfti að restarta ntp með sudo systemctl restart ntp.

  client1 og 2 voru þannig að downloada ntp með sudo apt install ntp.
  fara í sud vi /etc/ntp.conf og bæta við ntp server og bæta við restrict línu: 
  
  ![8 ntp client conf](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/ba0fa313-8725-47b7-84f3-c25bfbf3dd90)

  sama var gert hjá client2

  sjá virkni:
  server1:
  ![8  server1 date](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/6a4b6da4-9582-470e-bdb6-e5f6089da661)
  client1:
  
  ![8  client1 date](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/dfc849c0-44d2-4cc4-96e6-45d2b6310546)

  -- ---------------------------------------

9. Syslog install and confiigure:
    byrjaði á því að installa rsyslog með sudo install rsyslog

   næst var að uncommnet-a udp og tcp línurnar og opna fyrir þær:
   ![9  rsyslogconf](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/c1b1feb4-8d2e-4ff0-9194-34b58bd433c4)

   næst var að breyta í client endanum og bæta við *.*@192.168.100.10 til þess að senda öll logs frá client1 og 2 á serverinn. og þá var það byrjað að senda á server1 öll logs (náði ekki að breyta í proactive management og monitoring):
      
![9  client1 rsyslog](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/cfabe0cd-7b3f-47fe-a990-f1bfcfdabb8d)

  -- ----------------------------------------

  11. SSH using Rsa keys.
      byrja á að installa ssh server á server1: sudo at install openssh-server.
      Næst þurfti að búa til key með keygen á client1 og 2: ssh-keygen -t rsa
      ![11  keygen client1](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/12f6a606-0583-4ac3-a6e9-768a4a967585)

      svo þurfti að copy-a lykilinn á serverinn með: ssh-copy-id ubuntu@192.168.100.10
      ![11 copying key to server](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/b6a0efc0-9534-4f32-bdf1-a2d69643e2ea)

      sýna að þetta virkar:
      ![11  ssh virkni](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/6c80dec8-6650-4955-af7d-a388bd6667f9)

12. Það eina sem er opið á server1 er 22/tcp fyrir ssh og 53/tcp fyrir domain allt hitt var lokað:
    notaði nmap 192.168.100.10 til þess að kíkja hvað væri opið:
    ![13  oll lokud](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/6753006b-bae5-4c8a-9319-28f75df57180)







