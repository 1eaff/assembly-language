**实验 3：**

1. 将下面的程序保存为 t1.asm 文件，将其生成可执行文件 t1.exe。


2. 用 Debug 跟踪 t1.exe
   的执行过程，写出每一步执行后，相关寄存器中的内容和栈顶的内容。
   ```assembly
    assume cs:codesg

    codesg segment

        mov ax, 2000H       ; ax = 2000H
        mov ss, ax          ; ss = 2000H
        mov sp, 0           ; sp = 0000H
        add sp, 10          ; sp = 000AH
        pop ax              ; ax = [2000A] = 0000, sp = 000C, [ss:sp] = [2000C] = 0000
        pop bx              ; bx = [2000C] = 0000, sp = 000E, [ss:sp] = [2000E] = 0000
        push ax             ; [2000C] = ax = 0000, sp = 000C, [ss:sp] = [2000C] = 0000
        push bx             ; [2000A] = bx = 0000, sp = 000A, [ss:sp] = [2000A] = 0000
        pop ax              ; ax = [2000A] = 0000, sp = 000C, [ss:sp] = [2000C] = 0000
        pop bx              ; bx = [2000C] = 0000, sp = 000E, [ss:sp] = [2000E] = 0000

        mov ax, 4c00H
        int 21H

    codesg ends

    end
   ```

3. PSP 的头两个字节是 CD 20，用 Debug 加载 t1.exe，查看 PSP 的内容。

    ```shell
    C:\>debug t1.exe
    -r
    AX=FFFF  BX=0000  CX=0016  DX=0000  SP=0000  BP=0000  SI=0000  DI=0000
    DS=075A  ES=075A  SS=0769  CS=076A  IP=0000   NV UP EI PL NZ NA PO NC
    076A:0000 B80020        MOV     AX,2000
    -d 075A:0000
    075A:0000  CD 20 FF 9F 00 EA FF FF-AD DE 4F 03 A3 01 8A 03   . ........O.....
    075A:0010  A3 01 17 03 A3 01 92 01-01 01 01 00 02 FF FF FF   ................
    ```
