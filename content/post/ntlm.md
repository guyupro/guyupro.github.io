---
title: "ntlm"
date: 2024-12-27
tags: ["NTLM","python"]
draft: false
---

```bash
pip install pycryptodome
```

```python
from Crypto.Hash import MD4  
  
def ntlm_hash(password):  
    # 将密码编码为 UTF-16LE    password_utf16 = password.encode('utf-16le')  
    # 创建 MD4 哈希对象  
    hash_object = MD4.new()  
    # 更新哈希对象  
    hash_object.update(password_utf16)  
    # 获取哈希值  
    ntlm_hash = hash_object.digest()  
    # 将结果转换为十六进制字符串  
    return ntlm_hash.hex().upper()  
  
# 明文密码  
plaintext_password = "123456"  
# 计算 NTLM 哈希  
hash_result = ntlm_hash(plaintext_password)  
  
print(f"NTLM hash for '{plaintext_password}': {hash_result}")
```

