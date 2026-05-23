## [牛客] 出题需要构造(2026.5.12 se)
**核心标签**：`构造`、`矩阵坐标的循环移位`
>**题意简述**
>构造一个矩阵另每行每列只有一对1和2

### 我的死因
- 思考时忘却题目条件导致被罚时，考虑条件不充分，忘记极端条件

### 核心代码
```cpp
//极端条件！！！
if(n==1||m==1){
		cout<<"NO"<<endl;
		return;
	}
if(n&1){
		cout<<2<<endl;
		for(int i=1;i<=n;i++){
			tu[i][i] = 1;
			int tmp = i+1;
			if(tmp>n) tmp=1;
			tu[i][tmp] = 2;
		}
	}
else{
	cout<<1<<endl;
	for(int i=1;i<=n;i++){
		tu[i][i] = 1;
	}
	for(int i=1,j=n;i<=n,j>=1;i++,j--){
		tu[i][j]=1;
	}
}
```