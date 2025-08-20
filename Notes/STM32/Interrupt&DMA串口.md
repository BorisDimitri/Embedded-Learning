`轮询模式串口`：

​	调用 HAL_UART_Transmit() 发送一段数据时，

	1. CPU先把数据移到TDR（`发送数据寄存器`）中，
	2. `发送移位寄存器` 按照设定比特率转发为高低电平，过程中CPU一直检测发送移位寄存器中是否已经发送完成，直至完成或者超时，

​	

​	

`串口中断模式`：NVIC中触发USART2 global interrupt

​	用 HAL_UART_Transmit_IT()

		1. 发送数据寄存器中的数据移入发送移位寄存器后，CPU继续执行
		2. 发送数据寄存器发送完成后，触发“发送数据寄存器空”中断

接收时如果没有接收完会继续向下执行，所以可能会导致在下一次循环时，上次的数据还没有接收完，就又开启串口中断接收了

串口接收完成第一时刻执行的 HAL_UART_RxCpltCallback() 可以被重定义，用于完整收到数据后的处理



`串口DMA模式`：（Direct Memory Access）

在USART_2中设置开启DMA通道，选取地址自增，外设数据不必自增





`串口空闲中断`：

​	串口接收从忙碌转为空闲(idle 连续一个字节的时间未接收到数据)的时候才会触发，

​	HAL_UART_ReceiveToIdle_DMA(&huart2, receiveData, sizeof(receiveData))

​	 **注意**接收数组长度要足够

​	可以通过重定义 HAL_UARTEx_RxEventCallback() 来实现在输入完成后的处理

​	使用 HAL_UART_ReceiveToIdle_DMA() 后，不再调用RxCpltCallback() 回调

​	**注意** 输入数据达到最大的一半的时候也会触发HAL_UART_RxEventCallback() ，可以用__HAL_DMA_DISABLE_IT() 来实现禁用传输过半中断

