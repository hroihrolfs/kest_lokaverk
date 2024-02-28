# kest_lokaverk

1. a) setja hostname og domainname. við breytum /etc/hostname file til þess að breyta hostname-inu. sama hjá client1 og 2.
  command: sudo vi /etc/hostname
![1  etc_hostname file til að breyta hostname](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/919ae632-2eda-4dd4-b0b6-6a12033177e3)
![1 hostname](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/ed40626c-3f73-488f-ab38-d5a0f9044b69)

1. b) að setja domainname notaði ég resolvconf library og byrjaði að breyta /etc/resolvconf(resolv.conf.d/head og bætti við domain ddp.is.
   ![1 domainname-alvoru](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/b080e9d8-8ac8-48fc-a3e8-877ce0da1d61)

   næst var sudo resolvconf -u sem update-ar /etc/resolv.conf file og bætir domain ddp.is
   og að lokum er að breyta /etc/hosts með sudo vi og bæta við domain name:
   ![1 domainname_hostsfile](https://github.com/hroihrolfs/kest_lokaverk/assets/89214090/f647b3e5-97b9-4e19-bac7-199e00ce191a)
