### RV64各指令解释

本文是作为学习笔记来记录RV-ISA各指令的解释，会持续更新的。

---

#### RV32I

##### auipc-U

从20位U立即数中构建一个32位偏移量，低12位补0，然后将这个偏移量加到pc上。最终送入rd。

##### addi-I

addi rd rs1,simm12

12bits立即数符号拓展位32位，与rs1寄存器做加法运算，结果存回rd。

*addi rd rs1,0可以被当做mov指令*

##### jal-UJ

jal rd,simm21

立即数为21位立即数进行符号拓展至32位**然后与当前pc相加作为跳转pc地址**。（最低位恒为0，指令中只有【20：1】的立即数）同时把下一条指令的pc（即pc+4）写入rd中。

##### jalr-I

jalr rd,rs1,simm12

把12位立即数符号拓展至32位，然后与rs1的值相加作为pc跳转地址，同时把下一条指令的pc存入rd。

##### *ebreak*

Debugger用来切换加入debugger环境的。

##### *ecall*

用来调用system call

---

#### RV64I

##### ld-I

把存储器中64位数值写入到寄存器rd中。

##### sd-S

sd rs2 rs1 ,simm12

立即数为符号拓展12位，存储地址为（rs1+simm12），把rs2的64位数据写入存储器。