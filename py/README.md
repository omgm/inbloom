# inbloom (Python)

Package inbloom implements a portable bloom filter that can export and import
data to and from implementations of the same library in different languages.

This implementation is a C extension which wraps libbloom (https://github.com/jvirkki/libbloom)

## Usage

```python
import inbloom

bf = inbloom.Filter(entries=100, error=0.01)
bf.add("abc")
bf.add("def")

assert bf.contains("abc")
assert bf.contains("def")
assert not bf.contains("ghi")

bf2 = inbloom.Filter(entries=100, error=0.01, data=bf.buffer())
assert bf2.contains("abc")
assert bf2.contains("def")
assert not bf2.contains("ghi")
```

### Serialization

```python
import inbloom
import binascii

payload = '620d006400000014000000000020001000080000000000002000100008000400'
assert binascii.hexlify(inbloom.dump(inbloom.load(binascii.unhexlify(payload)))) == payload
```
