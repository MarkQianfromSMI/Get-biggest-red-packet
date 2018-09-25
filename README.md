# Get-biggest-red-packet
快手笔试题
/*
红包依次排列，有序或者无序均可，将红包队列切成三段，要求第一个和第三个红包的红包和相等且最大
仅供自己浏览，未写注释勿喷
*/

#include<iostream>
#include<cstdio>
#include<vector>

using namespace std;
int Array[100] = { 0 };

void swap(int a, int b)
{
	int t = a;
	a = b;
	b = t;
}

int MoneyGetMax(int n, int A[])
{
	int SumPre = 0, SumLast = 0;
	bool flag = false;
	vector<int> vec;
	for (int i = 0; i < n - 2; i++)
	{
		SumPre += A[i];
		for (int j = i + 2; j < n ; j++)
		{
			for (int last = j ; last < n; last++)
				SumLast += A[last];

			if (SumPre == SumLast)
			{
				flag = true;
				vec.push_back(SumLast);
				break;
				SumLast = 0;
			}
			SumLast = 0;
		}
		SumLast = 0;
	}
	if (flag == true)
	{
		int size = vec.size();
		for (int i = 0; i < size - 1; i++)
		for (int j = 0; j < size - i - 1; j++)
		if (vec[j] > vec[j + 1])
			swap(vec[j], vec[j + 1]);
		return vec[size - 1];
	}
	else
		return -1;

}

int main()
{
	int n, i=0, x, value;
	vector<int> vec1;
	cin >> n;
	for (int j = 0; j < n; j++)
	{
		scanf_s("%d", &x);
		Array[j] = x;
	}

	value = MoneyGetMax(n, Array);
	if (value != -1)
		cout << value;
	else
		cout << "input value is error !";
	system("pause");
	return 0;
}
