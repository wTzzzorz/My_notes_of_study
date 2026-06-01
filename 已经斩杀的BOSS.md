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

## [CF1050E]  Split (2026.5.18 third)
**核心标签** : `双指针`、`滑动窗口`

> **题意简述**
> 寻找多少个[l,r] 区间其中所有元素的出现次数不超过本身的总元素出现次数/k

### 我的死因
- 双指针的时候没想到超出的总是新加入的

### 核心代码
```cpp
while (hashi[a[r]] > windows_maxn[a[r]]) {
	hashi[a[l]]--;
	l++;
}
```



## [牛客] 出题需要加法（2026.5.18 th）
** 核心标签 **: `二进制`、`前缀计数`、`二分`、`预处理`

>  **题意简述**
>  寻找在区间 [L,R] 中所有数字在二进制的表示下只包含两个1或者是 $2^n$ 即一个数字$w = 2^x + 2^y$的个数

### 我的死因
- 推理了半天一步求出来的数学公式，应该去想怎么枚举的，没有考虑位运算的知识和优势
- 位运算要开1LL防止爆int

### 核心代码
```cpp
	for (int x = 0; x < 63; x++) {
		for (int y = x; y < 63; y++) {
			int val = (1LL << x) + (1LL << y);
			if (l <= val && val <= r) {
				cnt++;
			}
		}
	}

```
从题解抄的法二可以借鉴
```cpp
vector<int> vals;
//预处理所有合法的数字
void init() {
    for (int i = 0; i <= 62; ++i) {
        for (int j = 0; j <= i; ++j) {
            int val = (1LL << i) + (1LL << j);
            vals.pb(val);
        }
    }
    sort(vals);
}
//二分查找到L，R的然后减去即可
void solve() {
    int l, r;
    cin >> l >> r;
    auto calc = [&](int n) { return upper_bound(all(vals), n) - vals.begin(); };
    cout << calc(r) - calc(l - 1) << endl;
}
```
---

## [牛客] 出题需要魔法(2026.5.18 th)
** 核心标签**： `单调栈`、`补集计数`
>**题意简述**
>找到当前元素$x$两边的第一个大于他本身的数字，通过组合计算区间内有多少个包含x的子序列

### 我的死因
- 代码构造能力很差，基本五分钟敲定了思路，但是单调栈的写法很糟糕，并且没有想到可以用总集减去补集就是答案
- 找右边最大默认应该是n+1的地方呀

### 核心代码
``` cpp
 	vector<int> a(n + 1, 0);
    fors(i, 1, n) cin >> a[i];
    vector<int> L(n + 1, 0);
    vector<int> R(n + 1, n + 1);
    stack<int> st;
    fors(i, 1, n) {
        while (!st.empty() && a[st.top()] < a[i]) {
            st.pop();
        }
        if (!st.empty()) {
            L[i] = st.top();
        }
        st.push(i);
    }

    while(!st.empty()) st.pop();

    for(int i = n; i >= 1; i--) {
        while (!st.empty() && a[st.top()] < a[i]) {
            st.pop();
        }
        if (!st.empty()) {
            R[i] = st.top();
        }
        st.push(i);
    }


    fors(i, 1, n) {
        int total = i * (n - i + 1);
        int invisible = L[i] * (n - R[i] + 1);
        
        cout << total - invisible << " ";
    }
```