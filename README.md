# -
关于链表的基础知识

typedef struct LNode
{
	long id;
	char name[50];
	float score;
	struct LNode* next;
}LNode,*LinkList;

//算法步骤
//单链表初始化（1）生成新结点作头结点，用头指针L指向头结点 
//（2）头指针指针域置空

#include <stdio.h>
#include <stdlib.h>

// 不用typedef定义链表节点结构体
struct Node {
    int data;           // 节点数据
    struct Node* next;  // 下一个节点指针
};

// 初始化链表，创建头结点
struct Node* initializeLinkedList() {
    // 创建头结点
    struct Node* head = (struct Node*)malloc(sizeof(struct Node));
    if (head == NULL) {
        printf("内存分配失败\n");
        return NULL;
    }
    
    // 头结点不存储任何实际数据，将指针域置为空
    head->data = 0;
    head->next = NULL;

    return head;
}

int main() {
    // 初始化链表
    struct Node* head = initializeLinkedList();
    
    // 链表操作...
    
    return 0;
}


void InitList_L(LinkList& L)
{
	L = (LinkList)malloc(sizeof(LNode));//C++用的是new
	L->next = NULL;//链表头指针指针域置空
}
//判断L是否为空链表
int ListIsEmpty(LinkList L)
{
	if (L->next)
	{
		return 1;//表示非空
	}
	else
	{
		return 0;//表示空
	}
}
//销毁单链表
void DestroyList_L(LinkList& L)
{
	LinkList p;
	while (L)
	{
		p = L;//每一次删除前面的一个结点
		L = L->next;
		free(p);//删除结点
	}
}
//清空单链表（表存在，但无元素）
void ClearList(LinkList& L)
{
	LinkList p, q;
	p = L->next;
	while (p)//不能删头指针
	{
		q = p;
  		p = p->next;
		free(q);
	}
	L->next = NULL;//最后处理头指针
}
//计算链表长度
int ListLength_L(LinkList& L)
{
	LinkList q = L->next;//指向有意义的项（第一项）
	int i = 0;
	while (q)
	{
		i++;
		q = q->next;
	}
	return i;
}

//
struct ListNode {
	int val;
	struct ListNode* next;
};
struct ListNode* deleteDuplicates(struct ListNode* head)
{
	//ListNode p = head->next;//缺乏构造方法
	if (!head)
	{
		return head;//若内容为空，返回原值
	}
	struct ListNode* cur = head;//避免对head直接处理
	while (cur->next)//这个是访问下一项的值
	{
		if (cur->val == cur->next->val)
		{
			cur->next = cur->next->next;
		}
		else
		{
			cur=cur->next;//这个是移动指针位置
		}
	}
	return head;
}


//疑难解答

typedef struct BiNode
{
	TElemType data;
	struct BiNode* lchild, * rchild;
}BiNode,*BiTree;

*BiTree 表示 BiTree 是一个指针类型。在这个上下文中，BiTree 是一个别名，表示指向 BiNode 结构体的指针类型。

具体地说，由于 BiTree 是一个指向 BiNode 结构体的指针类型的别名，因此 *BiTree 表示对 BiTree 类型的指针进行解引用操作，得到指向 BiNode 结构体的实际指针。

例如，如果有一个 BiTree 类型的指针变量 T，可以使用 *T 来访问 BiNode 结构体中的成员变量。例如，可以使用 (*T)->data 来访问 BiNode 结构体中的 data 成员变量。

需要注意的是，这里的 *BiTree 表示指针类型，而不是指针变量。指针变量声明时需要加上 * 符号，比如 BiTree* T 声明了一个指向 BiNode 结构体的指针变量 T。

BiTree*T 和 BiTree T 是有区别的。

BiTree*T 表示 T 是一个指针变量，其类型是 BiTree，即指向 BiNode 结构体的指针变量。

BiTree T 表示 T 是一个普通变量，其类型是 BiTree，即 BiNode 结构体。

具体来说，假设 BiTree 是一个指向 BiNode 结构体的指针类型的别名，那么：

BiTree* T 声明了一个指向 BiNode 结构体的指针变量 T。
BiTree T 声明了一个普通变量 T，其类型是 BiNode 结构体。
在用法上也有所不同：

BiTree* T 可以通过 T 来访问指针所指向的 BiNode 结构体的成员变量，需要使用 -> 运算符进行访问，例如 T->data。
BiTree T 可以直接通过 T 来访问 BiNode 结构体的成员变量，使用 . 运算符，例如 T.data。
总结：BiTree*T 声明一个指针变量，而 BiTree T 声明一个普通的结构体变量。

//关于

void PreOrderTraverse(BiTree T) 和 void PreOrderTraverse(BiTree* T) 在参数传递方式上有区别。

void PreOrderTraverse(BiTree T): 这个函数接受的参数是一个指向 BiNode 结构体的指针类型的别名 BiTree，但在函数内部直接使用 T 来访问结构体成员。这意味着函数接受的是实际的结构体变量而不是指针，传递时会进行值传递，即传递的是变量的副本。


void PreOrderTraverse(BiTree T)
{
    // 使用 T 访问结构体成员
    // ...
}
调用函数时需要传递一个 BiNode 结构体变量的副本，例如：


BiNode node;
PreOrderTraverse(node);
在函数内部对 T 所作的修改不会影响到原始的结构体变量。

void PreOrderTraverse(BiTree* T): 这个函数接受的参数是一个指向 BiNode 结构体的指针的指针类型 BiTree*，在函数内部需要使用 *T 来访问结构体成员。这意味着函数接受的是指针的指针，传递时会传递指针的地址。


void PreOrderTraverse(BiTree* T)
{
    // 使用 *T 访问结构体成员
    // ...
}
调用函数时需要传递一个 BiNode 结构体指针的地址，例如：


BiNode* nodePtr;
PreOrderTraverse(&nodePtr);
在函数内部对 *T 所作的修改会影响到原始的结构体指针。

总结：void PreOrderTraverse(BiTree T) 接受变量副本作为参数，而 void PreOrderTraverse(BiTree* T) 接受指针的地址作为参数。在函数内部的使用方式和对原始变量的影响上有所不同。

#用数组表示链表
const int N = 10000;
int e[N], ne[N], head, idx;
//ne[N]储存的是下标
// 
////头插法
//void add(int*e,int x)
//{
//	head = 0;
//	int temp = e[head];
//	e[head] = x;
//	head++;
//	e[head] = temp;
//}
void add(int x)
{
	//全局变量一直在变
	e[idx] = x;
	printf("e[idx] = %d\n", e[idx]);
	ne[idx] = head;
	/*int temp = head;*/
	printf("ne[idx] = %d\n", ne[idx]);
	head = idx++;
	printf("head = %d\n", head);
}
void remove(int k)//移除第k个元素
{
	//ne[k]就是第k个元素的下标（k-1）
	//e[k + 1] = e[k];
	ne[k] = ne[ne[k]];
}

int main()
{
	head = -1;
	/*int nums[N] = { 1,2,3,1,1,3 };*/
	add(2);
	add(3);
	add(4);
	add(5);
	remove(1);
	/*char s[] = {'a','a', 'a', 'a', 'b'};
	char t[] = { 'b','b', 'b', 'b', 'a'};*/
	printf("----------------------------------1-------------\n");
	//指针的方法
	//head已经改变
	for (int i = head; i != -1; i = ne[i]) {
		printf("%d ", e[i]);
	}
	printf("\n");
	printf("----------------------------------2-------------\n");
	return 0;
}
