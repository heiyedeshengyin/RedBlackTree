# RedBlackTree
其它数据结构:  
树:[二叉树](https://github.com/heiyedeshengyin/BinaryTree) [二叉搜索树](https://github.com/heiyedeshengyin/BinarySearchTree) [AVL树](https://github.com/heiyedeshengyin/AVLTree)  
链表:[链表](https://github.com/heiyedeshengyin/LinkedList) [双链表](https://github.com/heiyedeshengyin/DoublyLinkedList)

### 简介
红黑树,由红黑两色结点组成的二叉搜索树,并且满足以下条件:  
1.树根始终为黑色  
2.外部结点均为黑色  
3.其余结点若为红色,则其孩子结点必为黑色  
4.从任一外部结点到根结点的沿途,黑结点的数目相等  

### 数据结构
#### 红黑树结点的颜色
```cpp
enum RBTreeColor
{
	RED,	//红色
	BLACK	//黑色
};
```

#### 红黑树的结点
```cpp
template <typename T>
struct TreeNode
{
	T key;	//结点中存储的数据
	RBTreeColor color;	//结点的颜色
	TreeNode<T>* left;	//结点的左孩子
	TreeNode<T>* right;	//结点的右孩子
	TreeNode<T>* parent;	//结点的父亲
	//结点的构造函数
	TreeNode(T x, RBTreeColor _color)
	{
		key = x;
		color = _color;
		left = nullptr;
		right = nullptr;
		parent = nullptr;
	}
};
```

#### 红黑树
```cpp
template <typename T>
class RedBlackTree
{
	TreeNode<T>* root;	//根结点
};
```

### 函数列表
#### 红黑树的成员函数
RedBlackTree();	//无参构造函数  
RedBlackTree(T x);	//创建一个根结点  
RedBlackTree(TreeNode\<T\>* _root);	//用一个已有的根结点赋值给根结点  
RedBlackTree(RedBlackTree\<T\> &_root);	//拷贝构造函数  
RedBlackTree(vector\<T\> v);	//用一个数组来创建红黑树  
~RedBlackTree();	//析构函数  
vector\<T\> PerOrderTraverse();	//先序遍历  
vector\<T\> InOrderTraverse();	//中序遍历  
vector\<T\> PostOrderTraverse();	//后序遍历  
vector\<T\> LevelOrderTraverse();	//层序遍历  
void clear();	//清空二叉树  
bool isEmpty();	//判断二叉树是否为空  
bool isBalanced();	//判断是否为平衡二叉树  
int height();	//获取树的高度  
int size();	//获取结点个数  
T maximum();	//获取最大值  
T minimum();	//获取最小值  
TreeNode\<T\>* search(T e);	//搜索结点  
bool insert(T e);	//插入节点  
bool remove(T e);	//删除结点  
T operator[] (int r);	//重载[]操作符  
RBTreeColor getColor(T e);	//获取结点的颜色  

#### TreeNode结点的操作函数
void destroyBiTree(TreeNode\<T\>* &root)  //销毁一个二叉树  
TreeNode\<T\>* copyBiTree(TreeNode\<T\>* &root) //复制一个二叉树到新的内存中  
void Per(TreeNode\<T\>* &root, vector\<T\> &v)  //先序遍历  
void In(TreeNode\<T\>* &root, vector\<T\> &v) //中序遍历  
void Post(TreeNode\<T\>* &root, vector\<T\> &v) //后序遍历  
bool isBalancedBiTree(TreeNode\<T\>* &root) //判断是否为平衡二叉树  
int getHeight(TreeNode\<T\>* &root) //返回二叉树的高度
int getSize(TreeNode\<T\>* &root) //返回二叉树中结点的个数
TreeNode\<T\>* getMax(TreeNode\<T\>* &root) //返回红黑树中存储最大值的结点  
TreeNode\<T\>* getMin(TreeNode\<T\>* &root) //返回红黑树中存储最小值的结点  
TreeNode\<T\>* searchIn(TreeNode\<T\>* &root, T val)  //搜索结点,若找到就返回该结点,若没找到就返回nullptr  
void leftRotate(TreeNode\<T\>* &root, TreeNode\<T\>* &x)  //对红黑树的节点(x)进行左旋转  
void rightRotate(TreeNode\<T\>* &root, TreeNode\<T\>* &y) //对红黑树的节点(y)进行右旋转  
void insertFixUp(TreeNode\<T\>* &root, TreeNode\<T\>* &node)  //红黑树插入修正函数  
void insertIn(TreeNode\<T\>* &root, TreeNode\<T\>* &node) //将结点插入到红黑树中  
void removeFixUp(TreeNode\<T\>* &root, TreeNode\<T\>* &node, TreeNode\<T\>* &parent)  //红黑树删除修正函数  
void removeAt(TreeNode\<T\>* &root, TreeNode\<T\>* &node) //删除红黑树中的结点  
ostream &operator<<(ostream &os, RedBlackTree\<T\> &m)  //重载<<操作符,按中序遍历输出红黑树结点的值和颜色  

### 一个主函数的例子
```cpp
#include "RedBlackTree.h"

int main()
{
	RedBlackTree<int> rbt1(12);
	rbt1.insert(1230);
	rbt1.insert(1231);
	rbt1.insert(1232);
	rbt1.insert(1233);
	rbt1.insert(121);
	rbt1.insert(120);
	rbt1.insert(125);

	cout << rbt1 << endl;
	cout << rbt1.height() << endl;
	cout << rbt1.size() << endl;

	rbt1.remove(125);

	cout << rbt1 << endl;
	cout << rbt1.height() << endl;
	cout << rbt1.size() << endl;

	RedBlackTree<int> rbt2(rbt1);
	rbt2.insert(123);
	rbt2.insert(124);
	rbt2.insert(125);

	cout << rbt2 << endl;
	cout << rbt2.height() << endl;
	cout << rbt2.size() << endl;

	RedBlackTree<int> rbt3(rbt2.search(1233));

	cout << rbt3 << endl;
	cout << rbt3.height() << endl;
	cout << rbt3.size() << endl;

	return 0;
}
```

### 参考资料
[红黑树(四)之 C++的实现](https://www.cnblogs.com/skywang12345/p/3624291.html)
