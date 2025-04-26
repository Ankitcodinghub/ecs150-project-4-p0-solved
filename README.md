# ecs150-project-4-p0-solved
**TO GET THIS SOLUTION VISIT:** [ECS150 Project 4  P0 Solved](https://www.ankitcodinghub.com/product/ecs150-p0-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;124844&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;ECS150 Project 4&nbsp; P0 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
ECS 150 – Project 4

Goal

The goal of this project is to implement the support for a very simple file system: ECS150FS.

Applications will have the possibility to read/write files from/to this file system.

int fs_mount(const char *diskname); /* Mounting the file system */ int fs_umount(void); int fs_info(void);

int fs_create(const charAssignment Project Exam

Help *filename); /* Creating files */ int fs_delete(const char *filename); int fs_ls(void); int fs_open(const char

int fs_write(int fd, void *buf, size_t count); /* Modifying files */ int fs_read(int fd, void *buf, size_t count);

Big picture: reality

Problem: the vast majority the file system management is in kernel mode!

Emulating a disk with a file

A disk, or a partition on a disk, merely represents contiguous binary data storage.

How can we easily emulate any size of contiguous data?… With a file!

$ dd if=/dev/zero of=emulated_disk_space bs=4K count=8192

$ ls -l emulated_disk_space

$ xxd emulated_disk_space 00000000: 0000 0000 0000 0000 0000 0000 0000 0000 …………….

00000010: 0000 0000 0000 0000 0000 0000 0000 0000

…………….Assignment Project Exam Help

00000020: 0000 0000 0000 0000 0000 0000 0000 0000 …………….

00000030: 0000 0000 0000 0000 0000 0000 0000 0000

0000 0000 0000 0000 0000 0000 0000 0000 …………….

00000060: 0000 0000 0000 0000 0000 0000 0000 0000

……………. 00000070: 0000 0000 0000 0000 0000 0000 0000 0000 …………….

00000080: 0000 0000 0000 0000 0000 0000 0000 0000 …………….Add

00000090: 0000 0000 0000 0000 0000 0000 0000 0000 ……………. …

01fffff0: 0000 0000 0000 0000 0000 0000 0000 0000 …………….

Big picture: replacing the disk

Accessing a file by blocks

#define BLOCK_SIZE 4096 int fd;

int block_open(char *disk_filename)

{

fd = open(disk_filename, O_RDWR); } int block_read(size_t block_nr, void *buf)

{ Assignment Project Exam Help

lseek(fd, block_nr * BLOCK_SIZE); read(fd, buf,

int block_write(size_t block_nr, void *buf)

{

lseek(fd, block_nr * BLOCK_SIZE);

}

Big picture: replacing the block device driver

Big picture: replacing the libc/vfs/fs drivers

Layout

Super Block FAT #0

Each block is 4096 bytes.

Add Layout

Super Block FAT #0

Each block is 4096 bytes.

Example with file system embedding 8192 data blocks: Amount of data blocks: 8192

Number of blocks for FAT: (8192 * 2) / 4096 = 4 Total amount of blocks: 1 + 4 + 1 + 8192 = 8198 Root directory block index: 5Add

Data block start index: 6

Superblock: high-level layout

Offset Length (bytes) Description

0x00 8 Signature (must be equal to “ECS150FS”)

0x08

2 Total amount of blocks of virtual disk

0x0A 2 Assi gnment Project Exam Help

Root directory block index

0x0C

art index

0x0E 2 Amount of data blocks

0x10

Number of blocks for FAT

0x11 4079 Unused/Padding

Superblock: at byte level

0x4 0x2 0x1 0x0

0x0000 1 S C E Beginningof block Signature

0x0004 S F 0 5

root dir idx total blocks

0x00080x000x05 0x20 0x06 total data blks data blk idx

0x0010Add 0x200x00 0x00 0x06

0x0010 xxx xxx xxx 0x04 FAT blocks

… End of

block0xFFFC xxx xxx xxx xxx

Superblock: C data structure

struct superblock{

???

};

Key points:

The integer types must match exactly those of the specificationCareful about alignment

Add

Digression

Integer types

Is char always 8 bits?

Is short int always 16 bits?

Is int always 32 bits? Etc.

Add

Integer types

Is char always 8 bits?

Is short int always 16 bits?

Is int always 32 bits? Etc.

Type SpecificationAssignment Project Exam Help

short “Capable of containing at least the [−32767, +32767] range; thus, it is at least

int “Capable of containing at least the [−32767, +32767] range; thus, it is at least 16 bits in size.”

long “Capable of containing at least the [−2147483647, +2147483647] range; thus, it is at least

32 bits in size.”

How to guarantee a certain size then? Integer types

Use integer types that have exact widths:

Add Structure alignment

#include &lt;stdint.h&gt;

int8_t int32_t Assignment Project Exam Help

Digressionint16_t

uint8_t uint16_t uint32_t

Structure naturally packed:

struct packed_s

{

int32_t a; int16_t b; int16_t c;

}; Assignment Project Exam Help

Add

Structure alignment

Structure naturally packed:

struct packed_s

{

int32_t a; int16_t b; int16_t c;

}; Assignment Project Exam Help

0x0000Add W 0x0004

Structure alignement

Structure fields have to aligned…

struct

padded_s

{

int8_t a; int32_t b; int16_t

c; }; Assignment Project Exam Help

Add Structure alignement

Structure fields have to aligned…

struct

padded_s

{

int8_t a; int32_t b; int16_t

c; }; Assignment Project Exam Help

0x4 0x2 0x1 0x0

Structure alignement

Force compiler to ignore alignment

struct packed_s

{

int8_t a; int32_t b; int16_t

c;

} __attribute__((packed));Assignment Project

Exam Help

Add Structure alignement

Force compiler to ignore alignment

struct packed_s

{

int8_t a; int32_t b; int16_t

c;

} __attribute__((packed));Assignment Project

Exam Help

https://.co0x4 0x2 0x1m0x0

eC hat pb

owco dera

padding

c b cont.

0x0000Add W

0x0004

Structure alignement

Conclusion: when transposing a specification into data structures, always use packing!

File format Network protocol Etc.

Add

Reading data structures from a file (or buffer)

Reading data from a file (or whatever blob of data), for which I know the layout. It can easily be type-casted into a structure instance.

struct packed_s

{

int32_t a; int16_t b; int16_t c;

};

Help

a

c b

0x4 0x2 0x1 0x0

0x0000

Assignment Project Exam

0x0004

char* buf[8]; fd = open(“file”,

O_RDWR);

read(bd, buf, 8); Add

struct packed_s *s = buf; s-&gt;a = 0;

/* or simply */ struct packed_s obj; read(bd, &amp;obj, sizeof(obj)); obj.a = 0;

FAT

Big array of 16-bit entries: linked-list of data blocks composing a file Three possible values for each entry:

0: corresponding data block is available

FAT_EOC: last data block of a file

!=0 &amp;&amp; !=FAT_EOC: index of next data block

Add

powcoderDescription

FAT

Big array of 16-bit entries: linked-list of data blocks composing a file Three possible values for each entry:

0: corresponding data block is available

FAT_EOC: last data block of a file

!=0 &amp;&amp; !=FAT_EOC: index of next data block

Root directory

1 block, 16-byte entry per file: 128 entries total

0x00 16 Filename (including NULL character)

0x10 4 Size of the file (in bytes)

0x14 2 Index of the first data block

0x16 10 Unused/Padding

Example: big file, small file, empty file

FAT Data blocks

&lt;test1, 25000, 2&gt;, 00

&lt;test2, 5000, 1&gt;,

&lt;test3, 0, FAT_EOC&gt; 11

… 22

33

44

Add 55

66

77

8

3

4

5

6

7

0xFFFF

test2, block #0

test1, block #0

test1, block #1

test1, block #2

test1, block #3

test1, block #4

test1, block #5

test2, block #1

0

0

8 0xFFFF

8

99

1010

Phase 1: Volume mounting

Add

Phase 2: File creation/deletion

fs_create(): Create a new file

Initially, size is 0 and pointer to first data block is FAT_EOC fs_delete(): Delete an existing file Don’t forget to free allocated data blocks fs_ls(): List all the existing files

Add

Phase 3: File descriptor operations

fs_open(): initialize and return file descriptor

32 file descriptors max

Can open same file multiple times Contains file’s offset (initially 0) fs_close(): close file descriptor fs_seek(): move file’s offset fs_stat(): return file’s size None of these function should change the file system…

Add

Phase 4: File reading/writing

Most complicated phase: might take as much time as all the previous phases combined

Allocation of new blocks must follow first-fit strategy (allocate first free data block from beginning of the FAT).

Three difficulties:

Small operations

First/last block on big operations Extending writes

Add

Small operation: example

Current offset is in the middle of the file, not aligned on the beginning of a block The size of data to read is smaller than what’s remaining in this block

char *buf

Data

Block

Current Size to offset be read

Might want to use a bounce buffer

Big operation: example

Current offset is in the middle of the file, not aligned on the beginning of a block

The size to read spans multiple (non-consecutive) blocks

The size of data to read is smaller than what’s remaining in the last block

char *buf

Data

Block

Current Size to offset be read

Mix of bounce buffer and direct copy

Extending write: example

Write more than what’s currently allocated

char *buf

Data

Implementation

Block

Add

Current Size to offset be written

In short

Think of all the cases: combination of file’s offset, file’s size, size to be read or written, etc.

Come up with a way to handle all these combinations in the most generic way (ie not one function per case!)

Add
