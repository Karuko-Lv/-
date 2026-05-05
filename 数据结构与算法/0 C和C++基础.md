## 结构体
```cpp
typedef struct [结构体标签名] { // 成员变量 } [类型别名];
```
`typedef` 的语法结构：`typedef [原类型] [新别名];`。
如果在 `struct` 后面没有写名字，这被称为**匿名结构体**。这种做法通常用于**结构体内部不需要引用自己**的情况。
```cpp
typedef struct {
    int x;
    int y;
} Point; 

// 之后可以直接用 Point 声明变量： Point p1;
```
###