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


