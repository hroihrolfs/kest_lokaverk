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


   
3. Static ip á server1. Ég notaði sudo vi /etc/netplan til þess að slökkva á dhcp og setja static ip:
![2 static_ip](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/5008f979-9d87-4804-b561-e6d4b4ce1dad)
