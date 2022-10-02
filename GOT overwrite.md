#### GOT Overwrite

- Our goal is to hijack the GOT entry for `puts` and have it instead invoke `system` 
- **Note** that we have to manunally specify a NUL byte terminator for `/bin/sh`.
	- would look like: `/bin/sh\x00`

---

#### Memory Leak Details:
```
  record                                        
┌─────────┐                                     
│         │            Global Offset Table      
│         │         ┌───────────────────────┐   
│         │         │         puts          │   
│         │    ┌───▶│                       │──┐
│         │    │    ├───────────────────────┤  │
│  name   │    │    │        printf         │  │
│         │    │    │                       │  │
│         │    │    ├───────────────────────┤  │
│         │    │    │          ...          │  │
│         │  leak   │                       │  │
│         │    │    └───────────────────────┘  │
├─────────┤    │                               │
│         │    │                               │
│ message │────┘                               │
│         │                                    │
└─────────┘      ┌─────────────────────────────┘
                 │                              
libc.so.6────────┼───────────────────────────┐  
│  ┌─────┐       │             ┌───────┐     │  
│  │puts │◀──────┘             │system │     │  
│  └─────┘                     └───────┘     │  
│                                            │  
│              ┌───────┐                     │  
│              │printf │                     │  
│              └───────┘                     │  
└────────────────────────────────────────────┘
```
- this will leak the real address of `puts`, by leveraging its presence in the Global Offset Table.
- The next bit of data will leak a pointer to `puts` from the GOT
- After that character, the next four bytes will be the **REAL address of `puts` in libc**.

---

### Preforming a GOT Overwrite
- find the OFFSET of `puts`, and use that to calculate the **ACTUAL base address** of `libc.so`.
- With the real loaded address of libc set in `libc.address`, the address for `libc.symbols.system` is automatically updated.
	- overwrite `puts` in the Global Offset Table. From here forward, all calls to `puts()` will instead call `system()`


- **calculating system()**
```python
# Calculate the base address of libc so we can calculate system()
libc = context.binary.libc
libc.address = got_puts - libc.symbols.puts
info("libc == %#x", libc.address

# Calculate system()
system = libc.symbols.system
info("system == %#x", system)
```
