# TCP - `Transmission Control Protocol`

## 协议头

![Image](https://chronosc.github.io/images/tcp-header.png)

### `Source Port` - 源端口，16位

### `Destination Port` - 目的端口，16位

### `Sequence Number` - 序列号，32位
* 如果`SYN`标志设置为(1)，则表示这是初始化序列号。第一个实际数据字节和此`SYN`相应的确认序列号`Acknowledgment Number(ACK)`等于此序列号加1
* 如果`SYN`标志设置为(0)，则表示这是在当前连接中该数据包的第一个数据字节的序列号，此序列号会不断累加

### `Acknowledgment Number` - 确认序号，32位

### `Data Offset` - 数据偏移，4位
以`字`(32位)(4字节）为计算单位，标识TCP报文段的实际数据起始处距离TCP报文段的起始处有多远。最小值为`5`，最大值为`15`，即最小`20 bytes`，最大`60 bytes`，这样即允许协议头有`40 bytes`的额外空间。

### `Reserved` - 保留字段，6位
保留为今后使用，目前应置为0。 

### `Flags` - 控制位，9位

* URG：紧急(urgent)，当`URG`＝1时，表明紧急指针字段有效,代表该封包为紧急封包。它告诉系统此报文段中有紧急数据，应尽快传送(相当于高优先级的数据)， 且`Urgent Pointer`字段也会被启用。

* ACK：确认(Acknowledge)。只有当`ACK`＝1时确认号字段才有效，代表这个数据包为确认数据包。当`ACK`＝0时，确认号无效。

* PSH：推送(Push function)若为1时，代表要求对方立即传送缓冲区内的其他对应封包，而无需等缓冲满了才送。

* RST：复位(Reset) ,当`RST`＝1时，表明TCP连接中出现严重差错（如由于主机崩溃或其他原因），必须释放连接，然后再重新建立运输连接。

* SYN：同步(Synchronous)，`SYN`置为1，就表示这是一个连接请求或连接接受报文,通常带有`SYN`标志的封包表示『主动』要连接到对方的意思。

* FIN：终止(Final)，用来释放一个连接。当`FIN`＝1时，表明此报文段的发送端的数据已发送完毕，并要求释放运输连接。

### `Window Size` - 窗口大小，16位
窗口的大小决定在不需要对端响应（acknowledgement）情况下传送数据的数量

### `Checksum` - 校验和，16位
当数据要由发送端送出前，会进行一个检验的动作，并将该动作的检验值标注在这个字段上； 而接收者收到这个数据包之后，会再次的对数据包进行验证，并且比对原发送的 `Checksum`值是否相符，如果相符就接受，若不符就会假设该数据包已经损毁，进而要求对方重新发送此数据包。在计算检验和时，要在TCP报文段的前面加上12字节的伪首部。

### `Urgent Pointer` - 紧急指针，16位
这个字段是在 Code 字段内的 URG = 1 时才会产生作用。可以告知紧急数据所在的位置(紧急指针指出在本报文段中的紧急数据的最后一个字节的序号)。

### `Options` - 选项，0-320位，按每32位切分
TCP首部可以有多达40字节的可选信息，用于把附加信息传递给终点，或用来对齐其它选项。目前此字段仅应用于表示接收端可以接收的最大数据区段容量，若此字段不使用， 表示可以使用任意数据区段的大小。 这个字段较少使用。

### `Padding` - 填充字段
如同IP封包需要有固定的32位表头一样，Options由于字段为非固定，所以需要 Padding字段用零来补齐。同样也是32位4字节的整数。

## 连接建立 - `3-Way Handshake`

TCP使用`三次握手`来建立一个连接。

`SYN` - `SYN & ACK` - `ACK`

## 连接终止 - `4-Way Handshake`

TCP使用`四次握手`来终止一个连接。

`FIN` - `ACK` - `FIN` - `ACK`