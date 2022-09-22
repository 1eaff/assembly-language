**实验 2：**

1. 使用
   Debug，将下面的程序段写入内存，逐条执行，根据指令执行后的实际运行情况填空。

   ```assembly
   mov ax, ffff
    mov ds, ax
    mov ax, 2200
    mov ss, ax
   
    mov sp, 0100
    ; ds = ffff, ss = 2200, sp = 0100
   
    mov ax, [0]         ; ax = [ffff0] c0ea
    mov ax, [2]         ; ax = [ffff2] 0012
    mov bx, [4]         ; bx = [ffff4] 30f0
    mov bx, [6]         ; bx = [ffff6] 2f31
   
    push ax             ; sp = 00fe, [220fe] = 0012
    push bx             ; sp = 00fc, [220fc] = 2f31
    pop ax              ; sp = 00fe, ax = 2f31
    pop bx              ; sp = 0100, bx = 0012
   
    push [4]            ; sp = 00fe, [220fe] = 30f0
    push [6]            ; sp = 00fc, [220fc] = 2f31
   ```

2. 仔细观察图 3.19 中的实验过程，然后分析：为什么 2000:0 - 2000:f
   中的内容会发生改变？

   TODO: 
