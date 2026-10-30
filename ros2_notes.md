C++ Vector 容器学习笔记
std::vector 是 C++ STL 中最常用的动态数组容器，支持随机访问，可以自动扩容。

0. 使用前提
cpp
#include <vector>
#include <algorithm> // 使用 for_each 等算法需要包含此头文件
using namespace std;
1. 创建与初始化
cpp
// 1. 默认构造：创建一个空的 vector
vector<int> v1; 

// 2. 区间构造：使用 [begin, end) 区间内的元素构造
// (注意：通常 v1 是已经存在的另一个 vector，或者数组)
vector<int> v2(v1.begin(), v1.end()); 

// 3. n个元素构造：创建 10 个值为 100 的元素
vector<int> v3(10, 100); 

// 4. 拷贝构造：用另一个 vector 初始化
vector<int> v4(v3); 

// 5. 赋值操作
vector<int> v5;
v5.assign(v1.begin(), v1.end()); // 将 v1 的区间数据赋值给 v5
// 补充：v5.assign(5, 10); 表示将 5 个 10 赋值给 v5
2. 容量与大小
cpp
vector<int> v;

v.empty();    // 判断容器是否为空 (返回 true/false)
v.capacity(); // 输出容器的容量 (不分配新内存能容纳的元素个数)
v.size();     // 输出容器当前元素的个数
v.resize(n1); // 重新指定大小为 n1。若变长，新位置用默认值(0)填充；若变短，超出部分删除。
v.resize(n1, n2); // 重新指定大小为 n1。若变长，超出部分用 n2 填充。
3. 插入与删除
cpp
vector<int> v;

// --- 尾部操作 ---
v.push_back(ele); // 在尾部插入元素 ele
v.pop_back();     // 删除最后一个元素

// --- 指定位置操作 (需要用到迭代器) ---
v.insert(v.begin(), ele); // 在指定迭代器位置插入 ele
v.insert(v.begin(), 5, ele); // 在指定位置插入 5 个 ele

v.erase(v.begin()); // 删除指定迭代器位置的元素
v.erase(v.begin(), v.end()); // 删除 [start, end) 区间内的元素
v.clear(); // 清空所有元素
4. 数据访问
cpp
vector<int> v = {10, 20, 30};

// ① 下标访问 [] (不检查越界，速度快)
int a = v[0]; 

// ② at() 访问 (会检查越界，越界抛出 out_of_range 异常，更安全)
int b = v.at(0); 

// ③ front() 返回第一个元素
int c = v.front(); 

// ④ back() 返回最后一个元素
int d = v.back(); 
5. 迭代器与遍历
笔记备注：迭代器类似于指针，可以通过解引用（*）来获取数据。

cpp
vector<int> v = {1, 2, 3};

// 起始迭代器：指向第一个元素
vector<int>::iterator itBegin = v.begin();
// 结束迭代器：指向最后一个元素的**下一个位置**
vector<int>::iterator itEnd = v.end();

// 传统 for 循环遍历
for (vector<int>::iterator it = v.begin(); it != v.end(); ++it) {
    cout << *it << " "; 
}

// 特殊遍历方式：for_each (需要包含 <algorithm>)
void myPrint(int val) { cout << val << " "; }
for_each(v.begin(), v.end(), myPrint);
6. 其他重要操作
cpp
vector<int> v1 = {1, 2};
vector<int> v2 = {3, 4};

// 交换：互换 v1 和 v2 的内容
v1.swap(v2); 

// 预留空间：预留指定大小的空间，避免频繁扩容导致的内存拷贝和迭代器失效
v.reserve(1000); 

