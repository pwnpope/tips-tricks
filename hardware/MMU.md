####  Memory management unit


A **memory management unit** (**MMU**), sometimes called **paged memory management unit** (**PMMU**), is a `computer hardware` unit having all `memory references passed through itself`, primarily performing the translation of [virtual memory addresses](https://en.wikipedia.org/wiki/Virtual_address "Virtual address") to [physical addresses](https://en.wikipedia.org/wiki/Physical_address "Physical address")

---
##### VAS ( Virtual Address Space or Address Space )
- Set of ranges of virtual addresses that an OS makes available to a process.

--- 

##### VAS used in Linux & Windows

- For `x86 CPU's Linux 32-bit` allows splitting the user and kernel address ranges in different ways: 
	- 3G/1G user/kernel (defualt)
	- 1G/3G user/kernel 
	- 2g/2g user/kernel


- On [Microsoft Windows](https://en.wikipedia.org/wiki/Microsoft_Windows "Microsoft Windows") 
	- Microsoft Windows 32-bit, by default, only `2 GiB are made available to processes` for their own use. The other 2 GiB are used by the operating system. 

	- On later 32-bit editions of Microsoft Windows it is possible to extend the user-mode virtual address space to `3 GiB while only 1 GiB is left for kernel-mode` virtual address space by marking the programs as `IMAGE_FILE_LARGE_ADDRESS_AWARE` and `enabling the /3GB switch in the boot.ini file`.

	- Microsoft Windows 64-bit
		- in a process running an executable that was linked with `/LARGEADDRESSAWARE:NO`, the operating system artificially `limits the user mode portion of the process's virtual address space to 2 GiB`.
		
		- `This applies to both 32-bit and 64-bit executables Processes running executables that were linked with the /LARGEADDRESSAWARE:YES` option.
			
			- `which is the default for 64-bit Visual Studio 2010 and later`, have access to **more than 2 GiB** of virtual address space: **up to 4 GiB for 32-bit executables**.
			- **up to 8 TiB for 64-bit executables in Windows through Windows 8**.
			- **128 TiB for 64-bit executables in Windows 8.1 and later**.

Allocating memory via [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)")'s [malloc](https://en.wikipedia.org/wiki/Malloc "Malloc") establishes the page file as the backing store for any new virtual address space. However, a process can also [explicitly map](https://en.wikipedia.org/wiki/Memory-mapped_file "Memory-mapped file") file bytes.


---


##### relationship between physical address space and virtual address space:

![alt text](https://upload.wikimedia.org/wikipedia/commons/3/32/Virtual_address_space_and_physical_address_space_relationship.svg)
