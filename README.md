Необходимо запустить две виртуальные машины с GNU/Linux и обеспечить сетевую связность между ними. Можно использовать публичные облака, системы виртуализации на локальной машине (например, Virtualbox) или даже два физических компьютера, соединённых кабелем.
 
1.  Проверьте, что с одной машины вы можете пропинговать другую. Запустите на второй машине tcpdump и убедитесь, что вы видите бегающие пинги. Будьте аккуратны с ним, если подключены по SSH. (при необходимости настройте IP-адресацию вручную)
2.  Заблокировать на второй виртуалке входящие ICMP echo запросы при помощи iptables (nftables). Проверить - с первой виртуалки вторая теперь пинговаться не должна, а в tcpdump должны быть видны только ICMP echo request’ы.  Конфигурация фаервола должна восстанавливаться после перезагрузки машины. 
3.  Перезагрузите вторую виртуалку, убедитесь, что пинга нет.
4.  Найдите аргумент ping, который позволит явно отобразить потерянные пакеты в консоли вместо тишины.
5.  Запустите на второй виртуалке nginx со статической Hello, World страницей. Запросите эту страницу с другой виртуалки (curl, wget, lynx в помощь, если виртуалка без графического интерфейса).
6.  Заблокируйте на второй виртуалке запросы к nginx при помощи iptables (nftables). Убедитесь, что страница перестала открываться с первой виртуалки.
7.  Сохраните правила iptables и, перезагрузив вторую виртуалку, убедитесь в том, что конфигурация фаервола применилась - вторая виртуалка не должна отвечать ни на пинги, ни на запросы веб-страницы.




Create two Ubuntu VMs using VirtualBox

![Image Alt text](images/Two_VMS_Overview.png)


Create common network for Vms

![Image Alt text](images/Create_Common_Network.png)


Ip a VMs

![Image Alt text](images/Ipa_Both_Machines.png)


Ping each other 

![Image Alt text](images/Ping_Each_Other.png)


Create Iptables rule for DROP ICMP echo  

![Image Alt text](images/Iptables_And_Dump_Loss.png)


Save iptables configs using iptables-persistent

![Image Alt text](images/Save_Iptabels_Configs.png)


Show more info while ping 

![Image Alt text](images/Show_Loss_Packages.png)


Set up Nginx and curl

![Image Alt text](images/Nginx_Curl.png)


Nginx curl after new Iptables rule

![Image Alt text](images/Nginx_Curl_After_Iptables.png)



Save iptables configs using iptables-persistent

![Image Alt text](images/Save_Iptabels_Configs.png)


Make sure iptables rules save after reboot

![Image Alt text](images/Saved_Configs_After_Reboot.png)


