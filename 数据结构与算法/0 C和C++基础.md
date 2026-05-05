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
## `malloc` 和 `new`
以二叉树数据结构最标准定义为例子
```cpp
typedef struct BiTNode {
    int data;
    struct BiTNode *lchild, *rchild;
} BiTNode, *BiTree;
```
「PS」 `BiTNode` 是一个结构体（树的节点），而 `BiTree` 是一个指针（指向节点的指针，等价于 `BiTNode*`）
初始化需要在空树基础上插入根结点
### `malloc` 写法
```cpp
//1️⃣定义空树
BiTree root = null;
//2️⃣定义根结点
root = (BiTree)malloc(sizeof(BiTNode));
```