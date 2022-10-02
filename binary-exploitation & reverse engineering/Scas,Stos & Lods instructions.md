- SCAS
	- ##### https://www.felixcloutier.com/x86/scas:scasb:scasw:scasd
	- compares a byte, word, doubleword or quadword specified using a memory operand with the value in AL, AX, or EAX. It then sets status flags in EFLAGS recording the results. The memory operand address is read from ES:(E)DI register (depending on the address-size attribute of the instruction and the current operational mode). Note that ES cannot be overridden with a segment override prefix.

--- 

- STOS 
	- ##### https://www.felixcloutier.com/x86/stos:stosb:stosw:stosd:stosq
	- stores a byte, word, or doubleword from the AL, AX, or EAX register (respectively) into the destination operand. The `destination operand is a memory location`, the address of which is read from either the ESI:EDI or ES:DI register (depending on the address-size attribute of the instruction and the mode of operation). The ES segment cannot be overridden with a segment override prefix.

---

- LODS
	- Loads the `memory byte or word` addressed in the **destination register (DI, EDI)** into the AL, AX, or EAX register. Before executing the lods instruction, load the index values into the SI source-index register.
