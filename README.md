# eightqueen
#include<iostream>
using namespace std;
const int StackSize = 8;          //定义栈的最大高度（八）
template<class T>
class SeqStack                    //定义顺序栈模板类
{
public:
	SeqStack() { top = -1; }
	void Push(T x);
	void Pop();
	bool Empty();
	void PlaceQueen(int row);
	bool Judge();
	void Output();
private:
	int top;
	T data[StackSize];
	int count = 0;                //定义解法数目
};
template<class T>
void SeqStack<T>::Push(T x)           //入栈
{
	if (top >= StackSize - 1)  throw"上溢";
	top++;
	data[top]=x;
}
template<class T>
void SeqStack<T>::Pop()              //出栈
{
	if (Empty())  throw "下溢";
	top--;
}
template<class T>
bool SeqStack<T>::Empty()             //判断栈是否为空
{
	if (-1 == top)
		return true;
	else
		return false;
}
template<class T>
void SeqStack<T>::PlaceQueen(int row)        //在栈顶放置符合条件的值的操作,即摆放皇后
{
	for (int col = 0; col < StackSize; col++)    //穷尽列
	{
		Push(col);
		if (Judge())                 //判断摆放皇后的位置是否安全
		{
			if (row < StackSize - 1)     //若还没有放到第八个皇后，则进行下一个皇后的放置
				PlaceQueen(row + 1);
			else
			{
				count++;
				cout<<"第"<<count<<"种解法："<<endl;
				Output();
			}
		}
			Pop();                  //出栈，以免干扰下次结果
	}
}
template<class T>
bool SeqStack<T>::Judge()               //判断摆放皇后的位置是否安全
{
	for (int i = 0; i < top; i++)                      //依次检查前面各行的皇后位置
	{
		if (data[top] == data[i] || abs((data[top] - data[i])) == (top - i))  //判断是否在同一列同一斜线			
			return false;
	}
	return true;
}
template<class T>
void SeqStack<T>::Output()
{
	for (int j = 0; j < 8; j++)
	{
		for (int i = 0; i < 8; i++)
		{
			if (i == data[j])
				cout << 'Q';
			else
				cout << '*';
		}
		cout << endl;
	}
}
int main()
{
	SeqStack<int>s;
	s.PlaceQueen(0);
	return 0;
}
