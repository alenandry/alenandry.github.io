# Python Solutions

## convert pESn

```python
import hashlib

meid = input("Enter a MEID: ").upper()

bytes = bytearray.fromhex(meid)
s = hashlib.sha1(bytes)
# Decode the hex MEID (convert it to binary!)

pesn = "80" + s.hexdigest()[-6:].upper()
# Put the last 6 digits of the hash after 80

print("pESN: " + pesn)

```

