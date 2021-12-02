#include<stdio.h>
#include<stdlib.h>
#define MAX 9
using namespace std;
typedef struct node
{
    char data;
    struct node* lchild;
    struct node* rchild;
    int index;
}BiTNode, * BiTree;
typedef struct BiTNode_s
{
    char data;
    int lchild;
    int rchild;
}BiTNode_s, * BiTree_s;
int i = 1;
int j = 1;


void PreCreatBiTree(BiTree& T)
{
    ///按先序次序输入二叉树中结点的值（一个字符），创建二叉链表表示的二叉树T
    char ch;///结点的值
    if ((ch = getchar()) == '*')///用*表示空
        T = NULL;///递归结束，建空树
    else
    {
        T = (BiTNode*)malloc(sizeof(BiTNode));///开辟新的空间
       // T->data = ch;///生成根结点赋值
        T->data = ch;///生成根结点赋值
        PreCreatBiTree(T->lchild);///递归创建左子树
        
        PreCreatBiTree(T->rchild);///递归创建右子树
    }
}



void PreTravel(BiTree& T)
{
    if (T)
    {
       // T->index = j++;  //根据先序创建下标
        printf("%c ", T->data);///中
        PreTravel(T->lchild);///先左子树
        PreTravel(T->rchild);///后右子树
    }
}

void MidTravel(BiTree& T)
{
    if (T)
    {
        MidTravel(T->lchild);
        printf("%c ", T->data);
       // T->index=j++;  //根据中根遍历顺序创建下标
        MidTravel(T->rchild);
    }
}

void AftTravel(BiTree& T)
{
    if (T)
    {
        AftTravel(T->lchild);
        AftTravel(T->rchild);
        T->index = j++;   //根据后根遍历顺序创建下标
        printf("%c ", T->data);
    }
}


/*void TreeToArray(BiTree& T, BiTNode_s a[])
{
a[i].data = T->data;

    

    if (T->lchild) a[i].lchild = T->lchild->index;
    else a[i].lchild =0; //赋下标

    if (T->rchild) a[i].rchild = T->rchild->index;
    else a[i].rchild = 0;  //赋下标

    i++;
    if (T->lchild) {
        TreeToArray(T->lchild, a);
   }  //先左
    if (T->rchild) {
        TreeToArray(T->rchild, a);

    }  //再右子树遍历
} */ //先序

/*void TreeToArray(BiTree& T, BiTNode_s a[])
{
    if (T->lchild) {
        TreeToArray(T->lchild, a); 
   }  //先左
    a[i].data = T->data;  //再中

    if (T->lchild) a[i].lchild = T->lchild->index;
    else a[i].lchild =0; //赋下标

    if (T->rchild) a[i].rchild = T->rchild->index;
    else a[i].rchild = 0;  //赋下标
     
    i++;

    if (T->rchild) {
        TreeToArray(T->rchild, a);

    }  //再右子树遍历
}*/ //中序
void TreeToArray(BiTree& T, BiTNode_s a[])
{
    if (T->lchild) {
        TreeToArray(T->lchild, a);
    }  //先左
   
    if (T->rchild) {

        TreeToArray(T->rchild, a);
    }  //后右

    a[i].data = T->data;  //再中

    if (T->lchild) a[i].lchild = T->lchild->index;
    else a[i].lchild = 0; //赋下标

    if (T->rchild) a[i].rchild = T->rchild->index;
    else a[i].rchild = 0;  //赋下标

    i++;

    
}   //后序

int main()
{
   
    BiTree T;
    BiTNode_s a[MAX];
    printf("请按先序遍历顺序输入二叉树的各节点，没有的用符号*代替：\n");
    PreCreatBiTree(T);
    printf("前序遍历结果：\n");
    PreTravel(T);
    printf("\n");
    printf("中序遍历结果：\n");
    MidTravel(T);
    printf("\n");
    printf("后序遍历结果：\n");
    AftTravel(T);
    printf("\n");
    TreeToArray(T, a);
    printf("转化成静态二叉链表为：\n");
    for (j = 1;j < MAX;j++)

        printf("%d %c %d %d\n", j, a[j].data, a[j].lchild, a[j].rchild);
    

    return 0;
}

///`ABCD***E**FG*H***
