Брандмауэр UFW


Брандмауэры, они же фаерволы, они же межсетевые экраны – это программы для фильтрации сетевого трафика. Брандмауэр регулирует, какие приложения могут получать данные извне через порт, сетевой интерфейс или в зависимости от IP источника, а к какие – нет. Благодаря этому создается дополнительная защита, что важно для серверов.

UFW (uncomplicated firewall – несложный фаервол) на самом деле не брандмауэр, а интерфейс к IPTables. В свою очередь, утилиту iptables также часто называют брандмауэром, хотя она является интерфейсом управления к Netfilter.

Netfilter – это межсетевой экран Linux, настраиваемый через iptables. Настраивать правила фильтрации трафика через iptables относительно сложно, поэтому используют утилиту ufw, которая позволяет упростить процесс настройки.

Обычно в linux-системах ufw устанавливается по-умолчанию, а на VPS его обычно включает и первоначально настраивает хостер. По умолчанию же ufw выключен.

Некоторые программы, принимающие по сети данные, прописывают в ufw свои так называемые профили. Зарегистрированными таким образом сервисами можно управлять, обращаясь к ним по именам. Профили содержатся в каталоге /etc/ufw/applications.d/:



Чтобы посмотреть список зарегистрированных профилей используется команда ufw app list  
 

Если файла приложения нет в /etc/ufw/applications.d/, это не значит, что оно не может получать данные по сети. Чтобы увидеть список всех программ, способных это делать, используется команда ufw status

```ufw status```  

В примере трафик, приходящий по протоколу SSH, разрешен, так как OpenSSH находится в статусе ALLOW (позволять). Когда стоит DENY (отвергать), разрешить сервису получать данные можно командой
ufw allow имя_сервиса. Например, ufw allow OpenSSH.

Если приложение не имеет профиля в /etc/ufw/applications.d/, то можно указать номер порта, которым пользуется соответствующее приложение или его имя. В случае протокола SSH команды могут быть такими:

```ufw allow ssh```  
или

```ufw allow 22```  
В дальнейшем, при установке веб-сервера Apache или любого другого, трафик через него надо будет разрешить в ufw. Свой профиль Apache регистрирует самостоятельно.

Если изначально брандмауэр выключен, то есть команда ufw status возвращает Status: inactive, следует выполнить такую серию команд:
```bash
sudo ufw default deny incoming  
sudo ufw default allow outgoing  
sudo ufw allow ssh  
sudo ufw enable  
```
Параметр enable переводит ufw в активный статус. Если потребуется выключить, используется disable. Вместо команды sudo ufw allow ssh лучше включать по имени профиля: sudo ufw allow 'OpenSSH'.
