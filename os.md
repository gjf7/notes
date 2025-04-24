1. Process
    - the illusion of its own memory (virtual address)
    - the illusion of its own CPU (thread)
2. ELF exectuable
    +-----------------------+
    |       ELF Header      |
    +-----------------------+
    |       .text           | （代码）
    +-----------------------+
    |       .rodata         | （只读数据）
    +-----------------------+
    |       .data           | （已初始化的全局变量和静态变量，占用磁盘空间，因为初始值需要存储在 ELF 文件中）
    +-----------------------+
    |       .bss            | （未初始化数据，不占磁盘空间，只记录大小）
    +-----------------------+
    |       ...             | （其他段，如 .symtab, .strtab 等）
    +-----------------------+
    
    ```c
    int global_var = 42;      // 存放在 .data
    static int static_var = 10; // 存放在 .data

    const int read_only_var = 100; // 存放在 .rodata
    char *str = "Hello, World!";  // 字符串 "Hello, World!" 存放在 .rodata
    // 多个相同的字符串常量可能会被合并（编译器优化）
    ```
3. 每一个 object 文件都包含一个符号表，linker 通过符号表将多个 object 文件链接在一起生成一个 a.out。

