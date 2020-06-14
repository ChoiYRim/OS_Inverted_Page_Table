# OS_Inverted_Page_Table

[CAUTION]

If you want to execute this source code on your computer, you have to run this software on 32bit Ubuntu Linux 16.04. In
addition, The size of physical memory of the 'SSUOS' which is OS for practice is 128MB and the size of one page frame is 4KB.

I'm not a native English speaker,so please consider it when you read this script. :)

[COPYRIGHT]

All copyright is belong to Soongsil University OS Lab and this project was fifth subject of OS class.

[OVERVIEW]

The main objects of this project have three parts. First of all, we need to understand 'Page Allocator'. Second of all, we
have to make 'Level Hash'. Last, we should make an 'Inverted Page Table'. In order to make this project, we need to comprehend
virtual memory, paging method, inverted page table, and level hash. If you understood these things, you have to make two
things that we have defined. I wrote detail to be made at [OBJECTS].

- Virtual Memory

Virtual Memory method allows a portion of disk can be used as expanded RAM. This method can expand an usable memory space by
loading unusing memory block to DISK. If the memory block saved in DISK is needed, it will be loaded to RAM once again and the
other memory block will be loaded to DISK. 'SSUOS' uses a real memory address by mapping a virtual memory through 'Page Table'
and 'Page Directory'. SWAP area owing to RAM space expansion is not used in SSUOS. (Actually, many OS currently used are
evolving towards like this.)

- Paging

Paging method is to manage the virtual memory into blocks of same size. A block with a certain size of virtual memory is
called a page,and a block with a certain size of physical memory is called a frame. Therefore, making a virtual memory means
that the OS should convert a page address referred by virtual memory to a frame address of physical memory. A virtual memory
address is a means to access to physical memory frame through a page table referred by virtual memory page number. The size of
page in SSUOS is 4KB and SSUOS uses a two-level table structure splited into page table and page directory.

- Inverted Page Table

![inverted]/(./image/inverted.png)

Inverted Page Table is a method to solve the problem that the space occupied by the page table increases when many processes
are created. It always uses an only certain portion of main memory regardless of the number of virtual page. There is one
inverted page table and one frame has only one entry corresponding to it. The part corresponding to the page number in the
virtual address uses the specific hash value from the hash function as the page index number. It uses a chaining hash since
multiple virtual addresses can point one entry.

- Level Hash

![hash]/(./image/hash.png)

Level Hash is a method to improve the memory writing performance. Level Hash consists of 2-level hash table of top level and
bottom level and top level hash table is 2 times larger than bottom level hash table. Two top level share one bottom level and
one hash table has 4 slots. There are two hash functions to access two differenct top buckets.

[OBJECTS]

1. Make a level hash

2. Make an Inverted Page Table using level hash
