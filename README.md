# 11.19.1
二叉树的非递归前序遍历（含堆栈）
// SY1807313_张东璇_第6次作业_非递归前序遍历.cpp : 定义控制台应用程序的入口点。
//

#include "stdafx.h"
#include<stdlib.h>
#include<iostream>
#include"Stack.h"
using namespace std;

struct Bitree*Create(void) {//按照前序遍历序列创建一个二叉树//
	struct Bitree*q;//创建根节点//
	q = (struct Bitree*)malloc(sizeof(struct Bitree));
	int x;
	cin >> x;
	q->date = x;
	if (x == 0) return NULL;
	cout << x << "->LiftTree= ";
	q->LiftTree = Create();
	cout << x << "->RightTree= ";
	q->RightTree = Create();
	return q;
}

void preOrder(struct Bitree*root) {//前序遍历非递归输出二叉树//
	Stack c;
	Bitree*p = root;//设置新结点指针p，将根节点赋值给p
	while (p != NULL) {
		cout << p->date << " ";
		if (p->RightTree != NULL) c.push(p->RightTree);//若有右子树，入栈（记忆）
		if (p->LiftTree != NULL) p = p->LiftTree;//若有左子树，遍历
		else {
			if (c.empty() == false) {//判断堆栈是否为空，为空时结束循环
				p = c.pop();//不为空，则出栈
			}
			else
				p = NULL;//结束循环
		}
	}
}

int main()
{
	Bitree *Root;
	Root = Create();
	cout << "非递归前序遍历结果为：";
	preOrder(Root);
	return 0;
}

#pragma once
struct Bitree
{
	int date;
	struct Bitree*LiftTree;
	struct Bitree*RightTree;
};
class Stack
{
public:
	Stack();
	~Stack();
	void push(Bitree*x);
	struct Bitree* pop();
	bool empty() const { //判断堆栈是否为空
		return count == 0;
	}
private:
	struct Node
	{
		struct Bitree* data;
		struct Node*next;
	};
	struct Node* top;
	int count = 0;
};

#include "stdafx.h"
#include "Stack.h"
#include<stdlib.h>

Stack::Stack()
{
}


Stack::~Stack()
{
}

void Stack::push(Bitree*x) {
	Node *p = new Node;
	p = (struct Node*)malloc(sizeof(struct Node));//申请一个新结点//
	p->data = x;
	p->next = top;
	top = p;
	count++;
}
struct Bitree* Stack::pop() {
	if (top == NULL)
		printf("Stack  is  empty!");
	else
	{
		count--;
		Node *p = new Node;
		Bitree*ch;
		p = (struct Node*)malloc(sizeof(struct Node));//申请一个新结点//
		p = top;                //暂时保存栈顶结点的地址//  
		ch = top->data;    //保存被删栈顶的数据信息//
		top = top->next;               //删去栈顶结点// 
		free(p);                          //释放被删结点//
		return(ch);
	}
}
