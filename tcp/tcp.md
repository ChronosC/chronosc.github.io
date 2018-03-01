# TCP - `Transmission Control Protocol`

## 协议头

![Image](https://chronosc.github.io/images/tcp-header.jpg)

* `Source Port (16 bits)` - 源端口，16位
* `Destination Port (16 bits)` - 目的端口，16位
* `Sequence Number (32 bits)` - 序列号
    * 如果`SYN`标志设置为(1)，则表示这是初始化序列号。第一个实际数据字节和此`SYN`相应的确认序列号`Acknowledgment Number(ACK)`等于此序列号加1
    * 如果`SYN`标志设置为(0)，则表示这是在当前连接中该数据包的第一个数据字节的序列号，此序列号会不断累加

## 连接建立 - `3-Way Handshake`

`SYN`-`SYN-ACK`-`ACK`

## 连接终止 - `4-Way Handshake`

`FIN`-`ACK`-`FIN`-`ACK`