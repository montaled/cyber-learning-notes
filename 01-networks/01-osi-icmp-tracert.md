## Wireshark

Что это за программа и зачем она нужна?

Программа для анализирования трафика и пакетов 

Как поймать свой ping: 
(какие действия по порядку: запуск захвата → ... → фильтр)
Запуск захвата → смотрю командную строку → закончился пинг → останавливаю захват → вверхняя строчка → icmp → все мои 8 пакетов.

Что я увидел после фильтра icmp:
(сколько строк и почему именно столько)

8 строк - 4 пакета получено 4 отправлено

Что внутри пакета:
(какие «конверты» есть и за что отвечает каждый)

> Frame ...                          ← общая информация о пакете (служебное, пропускаем)
> Ethernet II ...                    ← внешний конверт: доставка внутри твоей домашней сети(внешний конверт, доставка до следующего устройства в локальной сети по MAC-адресам)
> Internet Protocol Version 4 ...    ← конверт с IP-адресами: доставка через интернет
> Internet Control Message Protocol  ← само письмо: «я тут»

'''
Frame 151: Packet, 74 bytes on wire (592 bits), 74 bytes captured (592 bits) on interface \Device\NPF_{42E085B8-DC9D-4AA9-A77B-4FADF3799AF8}, id 0
Ethernet II, Src: ASUSTekCOMPU_84:5a:4b (60:cf:84:84:5a:4b), Dst: ASUSTekCOMPU_96:36:20 (08:bf:b8:96:36:20)
Internet Protocol Version 4, Src: 192.168.50.207, Dst: 8.8.8.8
    0100 .... = Version: 4
    .... 0101 = Header Length: 20 bytes (5)
    Differentiated Services Field: 0x00 (DSCP: CS0, ECN: Not-ECT)
    Total Length: 60
    Identification: 0x20bd (8381)
    000. .... = Flags: 0x0
    ...0 0000 0000 0000 = Fragment Offset: 0
    Time to Live: 128 - время жизни(пакет только начал идти)
    Protocol: ICMP (1) - протокол
    Header Checksum: 0x0000 [validation disabled]
    [Header checksum status: Unverified]
    Source Address: 192.168.50.207 - отправитель
    Destination Address: 8.8.8.8 - получатель
    [Stream index: 15]
Internet Control Message Protocol
'''

'''
Frame 152: Packet, 74 bytes on wire (592 bits), 74 bytes captured (592 bits) on interface \Device\NPF_{42E085B8-DC9D-4AA9-A77B-4FADF3799AF8}, id 0
Ethernet II, Src: ASUSTekCOMPU_96:36:20 (08:bf:b8:96:36:20), Dst: ASUSTekCOMPU_84:5a:4b (60:cf:84:84:5a:4b)
Internet Protocol Version 4, Src: 8.8.8.8, Dst: 192.168.50.207
    0100 .... = Version: 4
    .... 0101 = Header Length: 20 bytes (5)
    Differentiated Services Field: 0x00 (DSCP: CS0, ECN: Not-ECT)
    Total Length: 60
    Identification: 0x0000 (0)
    000. .... = Flags: 0x0
    ...0 0000 0000 0000 = Fragment Offset: 0
    Time to Live: 117 - время жизни(Time to Live: 117 — осталось после пути (128 − 117 = 11 роутеров).)
    Protocol: ICMP (1) - протокол 
    Header Checksum: 0x423a [validation disabled]
    [Header checksum status: Unverified]
    Source Address: 8.8.8.8 - отправитель
    Destination Address: 192.168.50.207 - получатель 
    [Stream index: 15]
Internet Control Message Protocol
'''

