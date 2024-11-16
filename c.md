1. extern and static:
    - extern: this thing is defined somewhere else
    ```c
    int x=10;            /* definition, can only appear once */
    extern int x;        /* declaration, explicitly not a definition */
    extern int x=10;     /* error!  Tries to have it both ways. */
    ```
    - static:
    |                 | defined inside procedure     | defined globally                     |
    | --------------- | ---------------------------- | ------------------------------------ |
    | STATIC used     | local scope, infinite extent | same-file scope, infinite extent     |
    | STATIC not used | local scope, local extent    | whole-program scope, infinite extent |


