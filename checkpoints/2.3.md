**检测点 2.3：**

下面的 3 条指令执行后，CPU 几次修改 IP？都是在什么时候？最后 IP 中的值是多少？

```assembly
    mov ax, bx      ; ax <- bx  IP <- IP + 3
    sub ax, ax      ; ax <- 0   IP <- IP + 3
    jmp ax          ; IP <- 0
```
