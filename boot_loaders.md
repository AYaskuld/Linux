Загрузчики

Когда компьютер выключен, его программное обеспечение (включая операционные системы, код приложения и данные) остается сохраненным в энергонезависимой памяти. Когда компьютер включен, на нем обычно нет операционной системы или ее загрузчика в оперативной памяти (ОЗУ). Компьютер сначала выполняет относительно небольшую программу, хранящуюся в постоянной памяти (ROM) вместе с небольшим объемом необходимых данных, для доступа к энергонезависимому устройству или устройствам, с которых программы и данные операционной системы могут быть загружены в оперативную память.

Небольшая программа, которая запускает эту последовательность, известна как bootstrap loader, bootstrap или boot loader. Единственной задачей этой небольшой программы является загрузка других данных и программ, которые затем выполняются из оперативной памяти. Часто используются многоступенчатые загрузчики, во время которых несколько программ возрастающей сложности загружаются одна за другой в процессе цепной загрузки.

### LILO

LILO входит в стандартную комплектацию всех дистрибутивов Linux. LILO старше и менее мощная. Изначально в LILO не было опции меню GUI.

### GRUB

Администрировать GRUB немного проще. Интерфейс командной строки, загрузка по сети, пароли MD5.

- /boot/grub/grub.conf /загрузка/grub.conf
- /etc/grub.conf

