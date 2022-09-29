**实验 5：**

1. 将下面的程序编译，连接，用 Debug 加载，跟踪，然后回答问题。

    ```assembly
    assume cs:code, ds:data, ss:stack

    data segment
        dw      0123h, 0456h, 0789h, 0abch, 0defh, 0fedh, 0cbah, 0987h
    data ends

    stack segment
        dw 0, 0, 0, 0, 0, 0, 0, 0
    stack ends

    code segment
        start:      mov ax, stack
                    mov ss, ax
                    mov sp, 16

                    mov ax, data
                    mov ds, ax

                    push ds:[0]
                    push ds:[2]
                    pop ds:[2]
                    pop ds:[0]

                    mov ax, 4c00h
                    int 21h
    code ends

    end start
    ```
    1. CPU 执行程序，程序返回之前，data 段中的数据为多少？

        ```assembly
        0123h, 0456h, 0789h, 0abch, 0defh, 0fedh, 0cbah, 0987h
        ```

    2. CPU 执行程序，程序返回之前，cs = `076c`, ss = `076b`, ds = `076a`。

    3. 设程序加载后，code 段的段地址为 X，则 data 段的段地址为 `X - 2`，stack
       段的段地址为 `X - 1`。

2. 将下面的程序编译，连接，用 Debug 加载，跟踪，然后回答问题。

    ```assembly
    assume cs:code, ds:data, ss:stack

    data segment
        dw      0123h, 0456h
    data ends

    stack segment
        dw 0, 0
    stack ends

    code segment
        start:      mov ax, stack
                    mov ss, ax
                    mov sp, 16

                    mov ax, data
                    mov ds, ax

                    push ds:[0]
                    push ds:[2]
                    pop ds:[2]
                    pop ds:[0]

                    mov ax, 4c00h
                    int 21h
    code ends

    end start
    ```

    1. CPU 执行程序，程序返回前，data 段中的数据为多少？

        ```assembly
        0123h, 0456h
        ```

    2. CPU 执行程序，程序返回前，cs = `076c`，ss = `076b`，ds = `076a`。

    3. 设程序加载后，code 段的段地址为 X，则 data 段的段地址为 `X - 2`，stack
       段的段地址为 `X - 1`。

    4. 对于如下定义的段：

        ```assembly
        name segment
        ...
        name ends
        ```

        如果段中的数据占 N 个字节，则程序加载后，该段实际占有的空间为 `ceil(X // 16)`。


3. 将下面的程序编译，连接，用 Debug 加载，跟踪，然后回答问题。

    ```assembly
    assume cs:code, ds:data, ss:stack

    code segment

    start:      mov ax, stack
                mov ss, ax
                mov sp, 16

                mov ax, data
                mov ds, ax

                push ds:[0]
                push ds:[2]
                pop ds:[2]
                pop ds:[0]

                mov ax, 4c00h
                int 21h
    code ends

    data segment
        dw      0123h, 0456h
    data ends

    stack segment
        dw      0, 0
    stack ends

    end start
    ```

    1. CPU 执行程序，程序返回前，data 段中的数据为多少？

        ```assembly
        0123h, 0456h
        ```

    2. CPU 执行程序，程序返回前，cs = `076a`，ss = `076e`，ds = `076d`。

    3. 设程序加载后，code 段的段地址为 X, 则 data 段的段地址为 `X + 3`，stack
       段的段地址为 `X + 4`。

4. 如果将 (1)，(2)，(3) 题中的最后一条伪指令 `end start` 改为
   `end`（也就是说，不指明程序的入口），则哪个程序仍然可以正确执行？请说明原因。

    仅有第 (3) 个。前两个会将 data 段中的数据错误的当代码去执行。

5. 程序如下，编写 code 段中的代码，将 a 段和 b
   段中的数据依次增加，将结果存到 c 段中。

    ```assembly
    assume cs:code

    a segment
        db      1, 2, 3, 4, 5, 6, 7, 8
    a ends

    b segment
        db      1, 2, 3, 4, 5, 6, 7, 8
    b ends

    c segment
        db      0, 0, 0, 0, 0, 0, 0, 0
    c ends

    code segment

    start:      mov cx, 8
                mov bx, 0

    s:          mov ax, a
                mov ds, ax
                mov dl, ds:[bx]

                mov ax, b
                mov ds, ax
                add dl, ds:[bx]

                mov ax, c
                mov ds, ax
                mov ds:[bx], dl

                inc bx
                loop s

                mov ax, 4c00h
                int 21h
    code ends
    end start
    ```

6. 程序如下，编写 code 段中的代码，用 push 指令将 a 段中的前 8
   个字型数据，逆序存储到 b 段中。

    ```assembly
    assume cs:code

    a segment
        dw      1, 2, 3, 4, 5, 6, 7, 8, 9, 0ah, 0bh, 0ch, 0dh, 0eh, 0fh, 0ffh
    a ends

    b segment
        dw      0, 0, 0, 0, 0, 0, 0, 0
    b ends

    code segment

    start:      mov ax, a
                mov ds, ax

                mov ax, b
                mov ss, ax
                mov sp, 16

                mov cx, 8
                mov bx, 0
    s:          push ds:[bx]
                add bx, 2
                loop s

                mov ax, 4c00h
                int 21h
    code ends

    end start
    ```
