## 硅谷live以太坊智能合约 第三课作业
这里是同学提交作业的目录

### 第三课：课后作业
- 第一题：完成今天所开发的合约产品化内容，使用Remix调用每一个函数，提交函数调用截图
- 第二题：增加 changePaymentAddress 函数，更改员工的薪水支付地址，思考一下能否使用modifier整合某个功能
- 第三题（加分题）：自学C3 Linearization, 求以下 contract Z 的继承线
- contract O
- contract A is O
- contract B is O
- contract C is O
- contract K1 is A, B
- contract K2 is A, C
- contract Z is K1, K2


---

### 1. 函数截图

各函数调用截图请见: [函数调用截图](images.pdf)


### 2. contract Z 继承线

```
L(O)  := [O]


L(A)  := [A] + merge(L(O), [O])
       = [A] + merge([O], [O])
       = [A, O]

L(B)  := [B] + merge(L(O), [O])
       = [B] + merge([O], [O])
       = [B, O]

L(C)  := [C] + merge(L(O), [O])
       = [C] + merge([O], [O])
       = [C, O]


L(K1) := [K1] + merge(L(B), L(A), [B, A])
       = [K1] + merge([B, O], [A, O], [B, A])
       = [K1, B] + merge([O], [A, O], [A])
       = [K1, B, A] + merge([O], [O], [O])
       = [K1, B, A, O]

L(K2) := [K2] + merge(L(C), L(A), [C, A])
       = [K2] + merge([C, O], [A, O], [C, A])
       = [K2, C] + merge([O], [A, O], [A])
       = [K2, C, A] + merge([O], [O], [O])
       = [K2, C, A, O]


L(Z)  := [Z] + merge(L(K2), L(K1), [K2, K1])
       = [Z] + merge([K2, C, A, O], [K1, B, A, O], [K2, K1])
       = [Z, K2] + merge([C, A, O], [K1, B, A, O], [K1])
       = [Z, K2, C] + merge([A, O], [K1, B, A, O], [K1])          // fail A, select K1
       = [Z, K2, C, K1] + merge([A, O], [B, A, O])                // fail A, select B
       = [Z, K2, C, K1, B] + merge([A, O], [A, O])
       = [Z, K2, C, K1, B, A] + merge([O], [O])
       = [Z, K2, C, K1, B, A, O]
```
