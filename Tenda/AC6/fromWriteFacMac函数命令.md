固件下载地址：https://www.tendacn.com/se/material/show/103794

版本：AC6 v2.0 Firmware_V15.03.06.51

漏洞点：web服务在处理post请求时，对mac参数没有进行过滤
<img width="851" height="257" alt="image" src="https://github.com/user-attachments/assets/7f81976a-5150-457e-822f-21175b636aa4" />

使用分号，可以执行命令
Gdb：
进入formWriteFacMac函数

<img width="865" height="414" alt="image" src="https://github.com/user-attachments/assets/87ee33eb-fa69-4b87-b7e2-f0afd7f03866" />

执行命令 cat /etc/passwd

<img width="828" height="267" alt="image" src="https://github.com/user-attachments/assets/d1620ca1-307c-4773-824c-59384bc53f44" />
看到密码
<img width="865" height="704" alt="image" src="https://github.com/user-attachments/assets/d15ecb8d-662c-4cf6-8624-c3512e13ff1d" />




