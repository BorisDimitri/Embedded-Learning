# TTL 串口

Two device connect through two data string (tx, rx)

`TX`: transmit IO port

`RX`: recieve IO port

normally, this two device should share the **same GND voltage**

two IO port switch its voltage level at a certain frequency

 `USART` : (Universal Synchronous/Asynchronous Receiver & Transmitter 通用同步异步接收器和发射器）

TTL Serial use the Asynchronous Receiver & Transmitter

`Baud Rate` : 每秒多少高低电平 

normally, there r a former bit and a end bit before and after transmit a byte

so in the  115200bit/s baud rate, we can transfer 11520 byte per second

 

