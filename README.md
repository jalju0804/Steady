# Steady
#include <stdio.h>

typedef struct Queue{
	int x;
	int y;
}Queue;

Queue queue[1000001];
int vis[305][305] = {0,};
int rear = 0;
int front = 0;
int xvect[8] = {2,1,-1,-2,-2,-1, 1, 2};
int yvect[8] = {1,2, 2, 1,-1,-2,-2,-1};

int main()
{
	int t;
	scanf("%d",&t);
	for(int i = 0;i<t;i++)
	{
		int tmp = 0;
		int n;
		scanf("%d",&n);
		int x1,y1;
		int x2,y2;
		scanf("%d %d",&x1,&y1);
		scanf("%d %d",&x2,&y2);
		
		queue[rear].x = x1;
		queue[rear++].y = y1;
		
		vis[x1][y1] = 0;
		if(x1 == x2 && y1 == y2) printf("0\n");
		else
		{
		while(rear >= front)
		{
			if(tmp == 1) break;
			int tmpx = queue[front].x;
			int tmpy = queue[front++].y;
			for(int i = 0;i<8;i++)
			{
				if(tmpy + yvect[i] >= 0 && tmpx + xvect[i] >= 0 && tmpx + xvect[i] < n && tmpy + yvect[i] < n && vis[tmpx+xvect[i]][tmpy+yvect[i]] == 0)
				{
					if(tmpx + xvect[i] == x2 && tmpy + yvect[i] == y2) {
						printf("%d\n",vis[tmpx][tmpy] + 1);
						tmp = 1;
						break;
					}
					else 
					{
						if(tmpx >= 0 && tmpy >= 0 && tmpx < n && tmpy < n)
						{
							queue[rear].x = tmpx + xvect[i];
							queue[rear++].y = tmpy + yvect[i];
							vis[tmpx+xvect[i]][tmpy+yvect[i]] = vis[tmpx][tmpy] + 1;
						}
					}
				}
			}
		}
		rear = 0;
		front = 0;
		for(int i = 0;i<n;i++)
		{
			for(int j = 0;j<n;j++)
			{
				vis[i][j] = 0;
			}
		
		}
		}
	}
	
	return 0;
}
