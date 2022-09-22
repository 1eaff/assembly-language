**检测点 3.2：**

1. 补全下面的程序，使其可以将 10000H～1000FH 中的 8 个字，逆序复制到 20000H～2000FH 中。逆序复制的含义如图 3.17 所示（图中内存里的数据均为假设）。
    ```assembly
    mov ax, 1000
    mov ds, ax

    mov ax, 2000
    mov ss, ax
    mov sp, 0010

    push [0]
    push [2]
    push [4]
    push [6]
    push [8]
    push [A]
    push [C]
    push [E]
    ```

1. 补全下面的程序，使其可以将 10000H～1000FH 中的 8 个字，逆序复制到 20000H～20000FH 中。

    ```assembly
    mov ax, 2000
    mov ds, ax

    mov ax, 1000
    mov ss, ax
    mov sp, 0000

    pop [E]
    pop [C]
    pop [A]
    pop [8]
    pop [6]
    pop [4]
    pop [2]
    pop [0]
    ```
