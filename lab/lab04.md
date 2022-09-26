**实验 4：**

1. 编程，向内存 0:200～0:23F 依次传送数据 0～63（3FH）。

```assembly
assume cs:code
code segment

    mov ax, 20h
    mov ds, ax
    mov bx, 0
    mov cx, 40h
s:  mov [bx], bx
    inc bx
    loop s

    mov ax, 4c00h
    int 21h
code ends
end
```

2. 编程，向内存 0:200～0:23F 依次传送数据 0～63（3FH），程序只能使用 9 条指令，9
   条指令包括 `mov ax, 4c00h` 和 `int 21h`。

*ommited.*

3. 下面的程序的功能是将 `mov ax, 4c00h` 之前的指令复制到内存 0:200 处，补全程序。

```assembly
assume cs:code
code segment
    mov ax, cs
    mov ds, ax
    mov ax, 0020h
    mov es, ax
    mov bx, 0
    mov cx, 17h
s:  mov al, [bx]
    mov es:[bx], al
    inc bx
    loop s
    mov ax, 4c00h
    int 21h
code ends
end
```
