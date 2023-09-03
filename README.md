# VLSI Physical Design for ASICs
## Objective
This GitHub repository focuses on VLSI Physical Design for ASICs using open-source tools. The main objective is to convert a logical design description (RTL - Register Transfer Level) into a physical layout suitable for integrated circuit fabrication. This transformation ensures that the circuit's functional representation translates into a physical form that meets design constraints, performance goals, and manufacturability standards. The entire flow is carried out using open source tools which includes the RISCV toolchain.

## SKILL OUTCOMES
### ASIC Flow
<img width="450" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/60e25599-543d-4f3b-87c9-392fc0aa02e0">

+ Architectural Design
+ RTL Design / Behavioral Modeling
+ Floorplanning
+ placement
+ clock Tree Synthesis
+ Routing

# COURSE
# DAY -1
## Introduction to Basic Keywords
<details>
<summary>Introduction</summary>
	
- **ISA (Instruction Set Archhitecture)**
  - ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.
  - It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.

- **RISC-V (Reduced Instruction Set Computing - Five)**.
  - It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
  - RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions. 

<img width="536" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e31d7c49-7160-443f-b73f-585cde8f3419">
</details>

<details>
<summary>From Apps to Hardware</summary>

1. **Apps:** Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.
2. **System software:** System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'
3. **Operating System:** The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

4. **Compiler:** A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

5. **Assembler:** An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

6. **RTL:** RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

 7. **Hardware:** Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.
</details>

<details>
<summary>Detail Description of Course Content</summary>

**Pseudo Instructions:** Pseudo-instructions are used to simplify programming, improve code readability, and reduce the number of explicit instructions a programmer needs to write. They are especially useful for common programming patterns that involve multiple instructions.
`Ex: li, mv`.

**Base Integer Instructions:** The term "base integer instructions" refers to the fundamental set of instructions that form the foundation for performing basic arithmetic, logical, and data movement operations.
`Ex: add, sub, and, or, xor, sll`.

**Multiply Extension Intructions:** The RISC-V architecture includes a set of multiply and multiply-accumulate (MAC) extension instructions that enhance the instruction set to perform efficient multiplication and multiplication-accumulate operations.
`Ex: mul, mulh, mulhu, mulhsu`.

**Single and Double Precision Floating Point Extension:** The RISC-V architecture includes floating-point extensions that provide support for both single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations. These extensions are often referred to as the "F" and "D" extensions, respectively. Floating-point arithmetic is essential for handling real numbers with fractional parts and for performing accurate calculations involving decimal values.

**Application Binary Interface:** ABI stands for "Application Binary Interface." It is a set of rules and conventions that govern how software components interact with each other at the binary level. The ABI defines various aspects of program execution, including how function calls are made, how parameters are passed and returned, how memory is allocated and managed, and more.

**Memory Allocation and Stack Pointer** 
- Memory allocation refers to the process of assigning and managing memory segments for various data structures, variables, and objects used by a program. It involves allocating memory space from the system's memory pool and releasing it when it is no longer needed to prevent memory leaks.
- The stack pointer is a register used by a program to keep track of the current position of the program's execution on the call stack. 
</details>

## Labwork for RISCV Toolchain
<details>
<summary>C Program</summary>

We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.

`leafpad sumton.c`
``` c
#include<stdio.h>

int main(){
	int i, sum=0, n=111;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}
```
Using the gcc compiler, we compiled the program to get the output.

`gcc sumton.c`
`.\a.out`

<img width="850" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/bd2cfc34-aeec-4c7d-81ce-6a902fe78a33">
</details>

<details>
<summary>RISCV GCC Compiler and Dissemble</summary>

Using the riscv gcc compiler, we compiled the C program.

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`

Using `ls -ltr sum1ton.c`, we can check that the object file is created.

To get the dissembled ALP code for the C program, 

`riscv64-unknown-elf-objdump -d sum1ton.o | less` .

In order to view the main section, type 
`/main`.
Here, since we used -O1 optimisation, the number of instructions are 15.

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/93402d4c-2c60-4499-93e7-57187b1636a7">

When we use -Ofast optimisation, we can see that the number of instructions have been reduced to 12.

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e3ad8b0f-ce56-4820-a3f0-8a3008d6a620">


- -Onumber : level of optimisation required
- -mabi : specifies the ABI (Application Binary Interface) to be used during code generation according to the requirements
- -march : specifies target architecture

In order to view the different options available for these fields, use the following commands

go to the directory where riscv64-unkonwn-elf is present

- -O1 : ``` riscv64-unkonwn-elf --help=optimizer```
- -mabi : ```riscv64-unknown-elf-gcc --target-help```
- -march : ```riscv64-unknown-elf-gcc --target-help```

For different instances,
- use the command ```riscv64-unknown-elf-objdump -d 1_to_N.o | less```
- use ``` /instance``` to search for an instance 
- press ENTER
- press ```n``` to search next occurance
- press ```N``` to search for previous occurance. 
- use ```esc :q``` to quit
</details>

<details>
<summary>Spike Simulation and Debug</summary>

`spike pk sum1ton.o` is used to check whether the instructions produced are right to give the correct output.

<img width="550" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f127a61f-99df-4eb1-87cd-8ac76f9baf77">


`spike -d pk sum1ton.c` is used for debugging.

The contents of the registers can also be viewed.

<img width="550" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/aeff2764-1f92-47ad-97d2-441bcbe2b95f">

- press ENTER : to show the first line and successive ENTER to show successive lines
- reg 0 a2 : to check content of register a2 0th core
- q : to quit the debug process
</details>

## Integer Number Representation 

<details>
<summary>Unsigned Numbers</summary>
	
- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
- Range: [0, (2^n)-1 ]
</details>

<details>
<summary>Signed Numbers</summary>
	
- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
- Range : Positive : [0 , 2^(n-1)-1]
          Negative : [-1 to 2^(n-1)]
</details>

<details>
<summary>Labwork</summary>

We wrote a C program that shows the maximum and minimum values of 64bit unsigned numbers.

``` c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```
<img width="650" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/ada3cb30-7388-422a-82bc-3db70ce41d5e">


We wrote a C program that shows the maximum and minimum values of 64bit signed numbers.
``` c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```

<img width="700" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/4561defd-7246-4a4a-97dc-d0c7b0d2f9e8">
</details>

# DAY - 2
## Application Binary Interface

<details>
<summary>Introduction to ABI</summary>
	
+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
</details>

<details>
<summary>Memmory Allocation for Double Words</summary>
	
64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly
1. **Little-Endian:**
In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. **Big-Endian:**
In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
#### For example, consider the 64-bit hexadecimal value 0x0123456789ABCDEF. 
In Little-Endian representation, it would be stored as follows in memory:

<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8c63e751-8882-4b1e-a2f8-84da628ee604">


In Big-Endian representation, it would be stored as follows in memory:

<img width="454" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3954540e-800f-4503-97ef-6c77daacd058">
</details>

<details>
<summary>Load, Add and Store Instructions</summary>
	
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.

Example `ld x6, 8(x5)`

In this Example
- `ld` is the load double-word instruction.
- `x6` is the destination register.
- `8(x5)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x8, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x8` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x9` is the destination register.
- `x10` and `x11` are the source registers.
</details>

<details>
<summary>2-Registers and their ABI Names</summary>
	
The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.
#### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components. 

<img width="430" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3b7aed64-37cd-492f-b9b5-cd840103566a">
</details>

## Labwork using ABI Function Calls
<details>
<summary>Algorithm for C Program using ASM</summary>
	
- Incorporating assembly language code into a C program can be done using inline assembly or by linking separate assembly files with your C code.
- When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
- The program executes the assembly function, following the assembly instructions you've provided.
</details>

<details>
<summary>Review ASM Function Calls</summary>
	
- We wrote C code in one file and your assembly code in a separate file.
- In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.

**C Program**
`1to9_custom.c`
  ``` c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
```
<img width="517" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/bc30c09e-f799-4741-8881-07870adec1bb">

`load.s`
``` s
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```
<img width="517" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/444090c4-0bd0-4669-b752-55cb4143cfed">
</details>

<details>
<summary>Simulate C Program using Function Call</summary>
	
**Compilation:** To compile C code and Asseembly file use the command

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o 1to9_custom.o 1to9_custom.c load.s` 

this would generate object file `1to9_custom.o`.

**Execution:** To execute the object file run the command 

`spike pk 1to9_custom.o`

<img width="800" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/8395e667-485a-414f-b51d-fee5028b5059">
</details>

# DAY - 3
## Introduction to open-source simulator iverilog

<details>
<summary>Introduction to iverilog design testbench</summary>
	
- **Simulator**
  - Simulator is the tool used for simulating the design and iverilog is the tool used for this course.
  - RTL design is checked for adherence to the spec by simulating the design.

- **Design**.
  - Design is the actual Verilog code or set of verilog codes which has the intended functionality to meet with required specifications.

- **Testbench**
  - Testbench is the setup to apply stimulus(test_vectors) to the design to check its functionality.
<img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/eb806b04-e6c0-4b03-8214-80cf0183ad76">

- **How simulator works?**.
  - simulator looks for the changes on the input signals.
  - Upon changes to the input the output is evaluated.
 
- **GTKWave**
  - Used for viewing the simulated waveforms.
    
- **iverilog based simulation flow**
<img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/0bbdc2e2-0b2a-4b26-8ed0-7eae4c7e3bf6">
</details>

## Labs using iverilog and gtkwave

<details>
<summary>Introduction to labs</summary>
	
- **Environment setup for running labs**
  
<img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1850bed7-a7db-46de-ba43-f850697d6e26">
</details>

<details>
<summary>Introduction to iverilog and gtkwave</summary>
	
- **Simulating 2:1 mux using iverilog and gtkwave**
- **Design**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/553ec117-c836-47ab-a63b-9bb064a91b38">

- **Testbench**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/6cc2b11f-f47b-4830-8bee-731da772712d">

- **Simulated waveform in gtkwave**
<img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/54e7f0aa-7967-461f-bfbc-6e47f649ff9f">

</details>

## Introduction to yosys and logic synthesis
<details>
<summary>Introduction to yosys</summary>

 <img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d35aae33-f873-4e82-a052-b111a9f6d733">
 
- **Synthesizer**
- A tool used for converting the RTL to netlist.
- Yosys is the synthesizer tool used in this course.

- **Synthesis**
- RTL to Gate level translation.
- The design is converted into gates and the connections are made between the gates.
- This is given out as a file called netlist.

- **What is .lib?**
- Collection of logic modules.
- Includes basic logic gates like AND, OR, NOT,etc.
- Different flavours of same gate.

- **Faster cells vs slow cells**
- load in digital logic circuit-> Capacitance
- Faster the charging/discharging of capacitance -> lesser the cell delay
  	- to charge/discharge the capacitance fast, we need transistors capable of sourcing more current.
  	- Wider transistors -> Low Delay -> More area and power as well.
  	- Narrow transistors -> More delay -> Less area and power
  	- Faster cells do not come free, they come at penalty of area and power.
</details>

## Labs using Yosys and Sky130 PDKs
<details>
<summary>Lab-1</summary>
	
- **Invoking yosys**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/c4f34f94-27e2-4f60-a6eb-55b6fe1b299b">

- **Synthesizing 2:1 mux**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/29f429af-ec5e-44db-898e-bcd4141b60d1">
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/2e049f37-0d9e-4fa1-9e61-946c2ef5e2e0">

- **Synthesis result**
<img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/81567934-02e3-4d54-ac2f-bf1eef1744d4">
</details>

<details>
<summary>Lab-2</summary>
	
- **Netlist with extra information**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e07fe6c3-966c-44f5-bd43-05a6786ed586">

- **Smaller netlist**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/763b3bc6-aa03-4b93-9180-c66719374dce">

</details>

# DAY - 4
## Introduction to timing .libs

<details>
<summary> Introduction to dot .lib </summary>

- **Contents in .lib file**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1c434a8f-cfea-4004-8a7a-85bff486261a">

- Frst line the .lib file contains
	- tt : indicates variations due to process and here it indicates Typical Process.
  	- 025C : indicates the variations due to temperatures where the silicon will be used.
  	- 1v80 : indicates the variations due to the voltage levels where the silicon will be incorporated.

- **Various parameters**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/b7527017-3e60-4c79-a5a8-3612c8555dd7">

- **Power consumption and area comparison**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/a6dc1db5-f6ab-4d84-8cab-7c6062e2a6b6">

</details>

## Hierarchical vs Flat Synthesis
<details>
<summary> Hierarchical Synthesis Flat Synthesis </summary>

- **Hierarchical Synthesis** - Hierarchical synthesis is an approach in digital design and logic synthesis where complex designs are broken down into smaller, more manageable modules or sub-circuits, and each module is synthesized individually. These synthesized modules are then integrated back into the overall design hierarchy. This approach helps manage the complexity of large designs and allows designers to work on different parts of the design independently.
- Here we use mutiple module.v and invoke yosys
<img width="700" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/942896f2-8a9d-44cf-bff6-e43774f9ac34">

- synth -top multiple_modules to set it as top module
<img width="400" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/cd097238-4a95-4f81-8865-003b0e41680e">

- To view the netlist show multiple_modules
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/aec962d9-7ad2-442c-a963-12c8e8439059">

- !gvim multiple_modules_hier.v
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/5c9256a2-06bf-4995-bd38-1437ba883b46">

- **Flattened Synthesis** - Flattened synthesis is the opposite of hierarchical synthesis. Instead of maintaining the hierarchical structure of the design during synthesis, flattened synthesis combines all modules and sub-modules into a single, flat representation
- netlist
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/4695badb-fd6e-4081-b29d-d8007e5a1627">

- !gvim multiple_modules_flat.v
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/87e0ba3b-156a-41cb-bc54-8f93e8f9ab60">

- **Sub Module level Synthesis** - Sub-module level synthesis is preferred when there are multiple instances of same module. Sythesizing the same module over several times may not be advantageous with respect to time. Instead, synthsis can be performed for one module, its netlist can be replicated and then stitched together in the top module. This is also used particulary in massive designs using divide and conquer method.

- Statistics
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1bd7dda1-37e5-43f3-8854-ae3f4f9b5626">

- Netlist
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/52421cf9-3299-4ada-a612-ba791e16d915">

</details>

## Various Flop Coding Styles and Optimization

<details>
<summary>Why Flops and Flop Coding Styles</summary>

**Why do we need a Flop?** 
- A flip-flop (often abbreviated as "flop") is a fundamental building block in digital circuit design.
- It's a type of sequential logic element that stores binary information (0 or 1) and can change its output based on clock signals and input values.
- In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed.
- During the propagation of data, if there are different paths with different propagation delays, then a glitch might occur.
- There will be multiple glitches for multiple combinational circuits.
- Hence, we need flops to store the data from the combinational circuits.

**D Flip-Flop with Asynchronous Reset** 
-  When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
-  Else, on the positive edge of the clock, the stored value is updated at the output.
  
+ `gvim dff_asyncres_syncres.v`
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/83d93978-474e-4a56-bcb9-539f48a02d35">

**D Flip_Flop with Asynchronous Set** 
-  When the set is high, the output of the flip-flop is forced to 1, irrespective of the clock signal.
-  Else, on positive edge of the clock, the stored value is updated at the output.
  
+ `gvim dff_async_set.v`
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/668b62b3-95ce-40e5-9937-a3301645cee4">


**D Flip-Flop with Synchronous Reset** 
-  When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
-  Else, on the positive edge of the clock, the stored value is updated at the output.
  
+ `gvim dff_syncres.v` 
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/10d89d8c-4d30-47f1-ac1f-938bf393356c">

**D Flip-Flop with Asynchronous Reset and Synchronous Reset** 
-  When the asynchronous resest is high, the output is forced to 0.
-  When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
-  Else, on the positive edge of the clock, the stored value is updated at the output.
-  Here, it is a combination of both synchronous and asynchronous reset DFF.

+ `gvim dff_asyncres_syncres.v`
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/63f16667-af33-4ac5-b5ee-e02c853a36c8">
</details>


<details>
<summary>Lab Flop Synthesis Simulations </summary>

**D Flip-Flop with Asynchronous Reset** 
-  Simulation
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/cb1a8093-e5e9-43f7-9b11-0b696e832185">

-  Synthesis
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/efb6c6d7-d703-47ba-a4e3-2d26a0700f11">


**D Flip_Flop with Asynchronous Set** 
-  Simulation
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/3574d670-cb92-470d-9f76-8835c019cabe">

-  Synthesis
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/59bae0f5-08b8-4925-a833-ceb022e3c999">

**D Flip-Flop with Synchronous Reset** 
-  Simulation
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f97f06b2-5e80-4487-8b11-384999452fa2">

-  Synthesis
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/874acc14-fa4e-4ddb-b07e-401cb5da8244">

</details>


<details>
<summary>Interesting optimisations </summary>

**mult_2** 
-  gvim mult_2.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/ff4e8959-ede4-41a9-a0c6-6e32ce365a26">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d65565a2-7014-4141-86ce-c569de580f67">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/7e3ba671-c5ef-4bcb-aac6-7ab95b02c87e">

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/6ff861d3-adc6-4488-9d97-0cd65eb049e5">

**mult_8** 
-  gvim mult_8.v

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1c87e450-e8e8-45fd-8171-38e3f9f83e6c">

-  Statistics
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/a347f5ad-b9d2-445e-acd2-f14c68b4d835">

-  Netlist
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e4cde78b-26c5-4d28-a23f-4dd6bbf435c9">

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/8c1d0c7e-3da1-4ff2-91fd-bb75fc88eabd">

</details>


# DAY - 5
## Introduction to Logic Optimizations

<details>
<summary> Combinational Logic Optimization </summary>
	
- **Combinational logic**
- Combinational logic refers to logic circuits where the outputs depend only on the current inputs and not on any previous states.

- **Types of Combinational Optimizations**
- Constant Propagation
- Boolean Logic Optimization. 

</details>


<details>
<summary> Sequential Logic Optimization </summary>
	
- **Sequential Logic**
- Sequential logic optimizations involve improving the efficiency, performance, and resource utilization of digital circuits that include memory elements like flip-flops and latches.

- **Types of Sequential Optimizations**
- Sequential Constant Propagation
- State Optimization
- Retiming
- Sequential Logic cloning(Floorplan aware synthesis)

</details>

## Combinational Logic Optimisations

<details>
<summary> opt_check </summary>
	
-  gvim opt_check.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/12fd204f-06dd-465a-adc1-80f1fff21b75">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f81b6c38-982a-487f-a4c4-4afa2cf86a50">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f2d45e9a-87f4-4fd8-b670-d4bee7d06750">

</details>

<details>
<summary> opt_check2 </summary>
	
-  gvim opt_check2.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/5ce627f7-3455-4add-b840-8a9e1ca81ebd">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/02ae9ced-5e9a-4aea-b92a-bc9c6cfd6463">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/9f964c30-fa98-48bb-bac9-fe8b18758ad7">

</details>

<details>
<summary> opt_check3 </summary>
	
-  gvim opt_check3.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/68b3b0c9-0999-4b85-9d77-5aeff4b0b703">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e2a968e2-8878-496e-86d2-716de521113a">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/a6ad0d4f-e15d-4a02-95b1-6a859559fee1">

</details>

<details>
<summary> opt_check4 </summary>
	
-  gvim opt_check4.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/b77631e4-e177-4662-ac97-dc7161048f61">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f1113645-47f1-4131-ad17-852795422647">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/4340cb4a-41b7-42ea-a6b5-760891410967">

</details>


## Sequential Logic Optimisations

<details>
<summary> dff_const1 </summary>
	
-  gvim dff_const1.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/cf213e78-5889-4388-924d-ca1eb91e12cd">

-  Simulation

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/6216ce5d-2c09-4de3-8260-e4c059372d23">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/48e04d09-1859-465f-b0f3-6f455f218a7f">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/6c4a19b2-c3e8-4212-9fc1-4ba3ee674880">

</details>

<details>
<summary> dff_const2 </summary>
	
-  gvim dff_const2.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d37028a4-f533-4bfe-9ffa-bd2b447b5f9a">

-  Simulation

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/931867bc-da58-4bec-b40a-9a7c64ade362">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f973f1d6-0dd0-4f7f-a758-b44d0855a17c">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/8af8dca9-ec06-419a-ac02-7030edb180b1">

</details>



<details>
<summary> dff_const3 </summary>
	
-  gvim dff-const3.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d9ab4a40-a1bd-433a-9551-acdc0529dcfc">

-  Simulation

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/b3e8dff0-5d28-484c-aeec-648f2365abbb">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d17a2988-45ab-4639-89bf-ef711a9f0215">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/ea8b0102-8a03-4328-a41a-9c4dae01b634">

</details>


<details>
<summary> dff_const4 </summary>
	
-  gvim dff_const4.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f5e15dcb-e47a-480f-b0f7-355e8be40aa5">

-  Simulation

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/94743cc9-4d69-4ec0-9ab7-3e461514f601">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/2e72a343-c07a-435b-be24-54cf08b5f280">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/77dff901-e622-4b8f-a8d0-2e15c98d939a">

</details>


<details>
<summary> dff_const5 </summary>
	
-  gvim dff_const5.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/be23bcfc-914e-4341-90b4-29e4848998f1">

-  Simulation

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/9b934bce-7898-43d8-8bd1-8e7b2ca1d0f9">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/739d6181-4901-4083-80be-fb92c5c84bf7">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/0cd6be80-c0f6-4ed9-a2cb-a0abf2cb3e39">

</details>

## Sequential Optimisations for Unused Outputs

<details>
<summary> counter_opt </summary>
	
-  gvim counter_opt.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/9869250b-d8b6-4b58-930c-b4a7bab31c27">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/6cbe7b44-d6eb-4bd9-86cf-ba63d362ae2f">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/8a74443f-c492-4c6b-b354-45fcd416bdfc">

</details>


<details>
<summary> counter_opt2 </summary>
	
-  gvim counter_opt2.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/771a532b-2363-4e04-bb7c-402352913348">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/487f3e7e-8df4-4d4c-a457-ce983a5544d5">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/ba5bc039-54cb-440e-94d4-0f2be4eda2d2">

</details>

# Day - 6
## GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements

<details>
<summary>GLS Concepts and Flow using Iverilog</summary>
	
**Gate Level Simulation (GLS)**
- Running the testbench against the synthesized netlist ouput as a DUT is known as Gate Level Simulation (GLS). The Output netlist should logically be same as the RTL code so that the testbench will align itself when we simulate both the files to obtain the waveforms.
- GLS is required to verify the logical correctness of the design post synthesis with the help of the netlist file. It ensures whether the timing of the design is met and for thi, the GLS used to run with delay annotations.
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1aebc269-44a0-4426-bab9-f55c2fe2ade5">

**Synthesis and simulation mismatch**
- If netlist is a true reciprocation of RTL, what is the need to validate the functionality of netlist? There may be synthesis and simulation mismatch due to the following reasons:
	-  Missing sensitivity list
 	-  Blocking vs non-blocking assignments
   	-  Non standard verilog coding

**Blocking statements**
- Executes the statements in the order in which they are coded

  ``` v
   module BlockingExample(input A, input B, input C, output Y, output Z);
    wire temp;

    // Blocking assignment
    assign temp = A & B;

    always @(posedge C) begin
        // Blocking assignment
        Y = temp;
        Z = ~temp;
    end
   endmodule
  ```
**Non - blocking statements**
- Executes the RHS of all such assignments when the always block is entered and assigned to LHS in a parallel evaluation.

  ``` v
    module NonBlockingExample(input clock, input D, input reset, output reg Q);

    always @(posedge clock or posedge reset) begin
        if (reset)
            Q <= 0;  // Reset the flip-flop
        else
            Q <= D;  // Non-blocking assignment to update Q with D on clock edge
    end
  endmodule
   ```
**Caveats with Blocking Statements**
- Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. Here are some important caveats associated with using blocking statements:
    - Procedural Execution: Blocking statements are executed sequentially in the order they appear within a procedural block (such as an always block). This can lead to unexpected behavior if the order of execution matters and is not well understood.
    - Lack of Parallelism: Blocking statements do not accurately represent the parallel nature of hardware. In hardware, multiple signals can update concurrently, but blocking statements model sequential behavior. As a result, using blocking statements for modeling complex concurrent logic can lead to incorrect simulations.
    - Race Conditions: When multiple blocking assignments operate on the same signal within the same procedural block, a race condition can occur. The outcome of such assignments depends on their order of execution, which might lead to inconsistent or unpredictable behavior.
    - Limited Representation of Hardware: Hardware systems are inherently concurrent and parallel, but blocking statements do not capture this aspect effectively. Using blocking assignments to model complex combinational or sequential logic can lead to models that are difficult to understand, maintain, and debug.
    - Combinatorial Loops: Incorrect use of blocking statements can lead to unintentional combinational logic loops, which can result in simulation or synthesis errors.
    - Debugging Challenges: Debugging code with many blocking assignments can be challenging, especially when trying to track down timing-related issues.
    - Not Suitable for Flip-Flops: Blocking assignments are not suitable for modeling flip-flop behavior. Non-blocking assignments (<=) are generally preferred for modeling flip-flop updates to ensure accurate representation of concurrent behavior.
    - Sequential Logic Misrepresentation: Using blocking assignments to model sequential logic might not capture the intended behavior accurately. Sequential elements like registers and flip-flops are better represented using non-blocking assignments.
    - Synthesis Implications: The behavior of blocking assignments might not translate well during synthesis, leading to potential mismatches between simulation and synthesis results.

</details>

## Labs on GLS and Synthesis-Simulation Mismatch

<details>
<summary> ternary_operator_mux </summary>	

+ `gvim teranry_operator_mux.v`

<img width="400" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d07cec10-e87e-433c-aaba-ac8e0f37c89f">

**Simulation**

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/719fbc77-3df1-42a0-b69e-31c0a3390109">

**Synthesis**

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/24307c4a-6cd5-4289-a24f-5e92aad17572">

<img width="400" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/af3e2061-60c5-41cc-9091-2fc2f0a7633d">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/88a08e63-ecb3-4e2c-949c-8f6ccc8f7fad">

</details>


<details>
<summary> bad_mux </summary>	

 + `gvim bad_mux.v`

 <img width="290" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/338505f3-a3a7-4443-b644-258c00006d49">

**Simulation**

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/ad719201-d7df-442c-8483-95cce74b5e9e">

**Synthesis**

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/4fedeeb0-11af-47da-8a43-aed80f8e378c">

<img width="400" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/142a9b05-579b-4036-8462-0bdf7bc6a706">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/c031d59f-0872-4f34-be78-3251c5501827">

</details>

## Labs on Synth-Sim Mismatch for Blocking Statement

<details>
<summary> blocking_caveat </summary>	

+ `gvim blocking_caveat.v`

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/a83c93ea-1581-4f07-a4c3-e6e92ccafcbf">

**Simualtion**

<img width="650" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/8dcbca09-24cb-4bca-a4ce-7cfbee7397e9">

**Synthesis**

<img width="327" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/36d41140-32b8-431e-a6c3-5c6d6b18c182">

<img width="400" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d9de9875-d386-4797-8139-1d5446b5ebbf">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v`

<img width="650" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/90dd0189-5493-43b2-9801-d614a7cd7b20">

</details>






