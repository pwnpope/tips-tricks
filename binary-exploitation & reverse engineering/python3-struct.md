### Struct library
- more: https://docs.python.org/3/library/struct.html
```python
from struct import *
```

- `pack`(_v1_, _v2_, _..._)[](https://docs.python.org/3/library/struct.html#struct.Struct.pack "Permalink to this definition")
	- Identical to the `pack()` function, using the compiled format. (`len(result)` will equal size)

- `pack_into`(_buffer_, _offset_, _v1_, _v2_, _..._)
	- Identical to the `pack_into()` function, using the compiled format.

- `unpack`(_buffer_)
	- Identical to the `unpack()` function, using the compiled format. The buffer’s size in bytes must equal size

- `unpack_from`(_buffer_, _offset=0_)
	- Identical to the unpack_from() function, using the compiled format. The buffer’s size in bytes, starting at position _offset_, must be at least size.

- `iter_unpack`(_buffer_)
	- Identical to the `iter_unpack` function, using the compiled format. The buffer’s size in bytes must be a multiple of size
`format`
- The format string used to construct this Struct object.
- Changed in version 3.7: The format string type is now `str` instead of `bytes`

- `size`
	The calculated size of the struct (and hence of the bytes object produced by the `pack()` method) corresponding to format
- `error`
	- Exception raised on various occasions; argument is a string describing what is wrong.

![alt text](https://i.imgur.com/Y2kQ7yl.png)

![alt text](https://i.imgur.com/KG2V554.png)


## parsing binary data

```python
import struct

example_string = b"\x00\x04\x00\x00\x00test"


class Example:
	def __init__(self):
		self.is_wide_string = False
		self.string_length = 0
		self.string = ""

	def from_buffer_copy(self, data):
		ptr = 0
		self.is_wide_string = struct.unpack("?", data[ptr:ptr+1])[0]
		ptr += 1
		self.string = struct.unpack("<I", data[ptr:ptr+4])[0]
		ptr += 4
		if self.is_wide_string:  # if 2 bytes
				self.string = data[ptr:ptr+(string_length+2)].decode("utf-16le") # utf-16 as little endian
				ptr += self.string_length * 2 
		else:
			self.string = data[ptr:ptr+self.string_length]
			ptr += self.string_length

	def packer(self):
		data = ""
		data += struct.pack("?", self.is_wide_string)
		data += struct.pack("<I", self.string_length)
		if self.is_wide_strings:
			elf.string = self.string.encode("utf-16le")
		else:
			data += self.string.encode("utf-8")
		return data

print("example string data: %r " % example_string)
es = Example()
es.from_buffer_copy()
print("example is wide: %s" % es.is_wide_string)


```
