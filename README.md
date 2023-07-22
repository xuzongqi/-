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
		q = p->next;
		free(p);
		p = q;
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
