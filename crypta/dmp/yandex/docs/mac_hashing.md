# Правила хеширования MAC-адресов

MAC-адреса должны хешироваться эквивалентно следующему примеру на Python:

```python
import binascii
import md5

mac_str='AE123456D0A1'
mac_bin=binascii.unhexlify(mac_str)
machash=md5.new(mac_bin).hexdigest().upper()
print machash # C5C32C30C07ABBB7580A0925D995FEE4
```
