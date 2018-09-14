# Project 0 Design Document

> Denison cs372  
> Fall 2018

## Author(s)

> Fill in your name and email address.

Emma Steinman <steinm_e1@denison.edu>

## Preliminaries

> If you have any preliminary comments on your submission, notes for the
> TAs, or extra credit, please give them here.

> Please cite any offline or online sources you consulted while
> preparing your submission, other than the Pintos documentation, course
> text, lecture notes, and course staff

## Report Sections
### Booting Pintos
-----------

#### QUESTIONS
> Put the screenshots of Pintos running in src/p0.
> A1: Is there any particular issue that you would like us to know?

#### Debugging

##### QUESTIONS: BIOS

> B1: What is the first instruction that gets executed?
>jump $0xffff0, $0xe05b

> B2: At which physical address is this instruction located?
>It is located at 0xffff0

> B3: Can you guess why the first instruction is like this?
>This is there to jump to the next section of code because the address
> is segmented. It will always jump to the BIOS.

> B4: What are the next three instructions?
> cmpl $0x0, %CS:0x6c48
> jne 0xfd2e1
> xor %dx, %dx

##### QUESTIONS: BOOTLOADER
> B5: How does the bootloader read disk sectors? In particular, what BIOS interrupt is used?
>It pushes the sector numbers to the stack in three parts, and searches through
> each partition on each drive while looking for partition of type 0x20. If it
> does not find one then it gives an interrupt of type 0x13.

> B6: How does the bootloader decides whether it finds the Pintos kernel?
> When it reaches a partition of type 0x20

> B7: What happens when the bootloader could not find the Pintos kernel?
> It prints not found and gives a BIOS interrupt 0x18

> B8: At what point does the bootloader transfer control to the Pintos kernel?
> It transfers control once the kernel is loaded when it reads the address and
> jumps to the correct location

##### QUESTIONS: KERNEL
> B9: Is there any issue in particular that you would like us to know?

### Kernel Monitor
-----------

#### DATA STRUCTURES

> C1: Copy here the declaration of each new or changed `struct` or
> `struct` member, global or static variable, `typedef`, or
> enumeration.  Identify the purpose of each in 25 words or less.

#### ALGORITHMS

> C2: Explain how you read and write to the console for the kernel monitor.
> I created a string into which I read the input and continuously check for a
> return character. If it is not a return, I add the character to the string. Once
> I see a return, I check the string to see if it is equal to whoami or quit and
> respond accordingly. After printing my name, I freed the array, and initialize
> a new one to collect new characters. If the user types exit, I break from the
> while loop to close the kernel.  

> C3: Any additional enhancement you implemented?
