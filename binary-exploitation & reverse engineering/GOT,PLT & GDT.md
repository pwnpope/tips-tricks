
#### GOT 
- this is the actual table of offsets as filled in by the linker for external symbols

-  `_GLOBAL_OFFSET_TABLE_` is used to locate the real addresses of **globals** (functions, variables etc) for PIC (Position-Independent Code), its commonly referred to as the GOT, you can read up on it here and a more indepth one here.

- independent of the memory address where the program's code or data is loaded at `runtime`

- It maps symbols in programming code to their corresponding `absolute memory addresses` to facilitate `Position Independent Code(PIC)`  and `Position Independent Executables` which are loaded to a different memory address each time the program is started.

---

#### PLT
- used to call `external functions` whose address isn't known in the time of linking

- Instead of calling `puts()` directly, the `.plt` section contains a special entry that points to the loader.
	- The loader then has to`resolve the actual address of the function`. Once it has done that it `updates an entry in the Global Offset Table` (GOT).



#### GDT
- ``(Global Descriptor Table)`` Every 8-byte entry in the GDT is a descriptor, but these descriptors can be references not only to `memory segments` but also to `Task State Segment`
	- Task State Segment holds information about a task
