# 剑指offer09栈与队列


* 题目：
[两个栈实现一个队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

* 相关点
栈 队列的数据结构 
C++ 栈与队列底层实现

* **stack 先入后出**

底层其实是利用顺序容器构造的一种容器适配器。

`  template<typename _Tp, typename _Sequence = deque<_Tp> >`

很明显，实现栈是通过双端队列的接口来提供不同的功能接口。

`* top() 
* push(valueType x)
* pop()
* swap(stack& _s)
* empty()
* emplace()`

内部点： 栈是一种先入后出的结构，在C++ STL 库中，利用其已实现的deque构造这种栈。
也就是只在一端入，利用
 `deque.push_back(), deque.pop_back(), deque.back() deque.empty() deque.emplace_back()`
方法提供stack的方法。这其中根据C++版本不同，移动对象到栈顶，和构造对象等有所不同。

* **queue 队列 先入先出**
queue 与 deque不同的是，这是一个单向的队列。
**解决思路：**
两个栈。
插入，只插入栈1。
删除   栈2 为空时，栈1不为空则把元素谈到栈2，栈2栈顶元素即为第一个入栈元素
栈2 为空， 栈1为空，说明队列为空。
栈2 不为空，直接删除栈2内容。

* C++ 代码实现：

**头文件：**
```
#include<iostream>
#include<stack>
template <typename T> 
class Cqueue{
public:
    Cqueue();
    ~Cqueue();
    void appendTail(const T& node);
    T deleteHead();
private:
    std::stack<T> s1;
    std::stack<T> s2;
};
```

**cpp文件**：

```
template<typename T>
T Cqueue<T>::deleteHead()
{
    // 
    if(s2.empty())
    {
        if(s1.empty())
        {
            return -1;
        }
        else{
            while(!s1.empty())
            {
                s2.push(s1.top());
                s1.pop();
            } 
        }
    }
    tem = s2.top();
    s2.pop();
    return T;
}
```   
