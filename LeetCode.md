# LeetCode



## 代码片段

```rust
// 除以2 n>>1
// 计算一半并向下取整 (n-n&1)/2    (n-n&1)>>1
// 计算两个数的中间值（平均数）(r-l)/2+l   ((r-l)>>1)+l  （先减后加不会有溢出危险）
```



## 欧拉筛和埃氏筛（在特定范围内找出所有的素数）

> 埃氏筛 把素数的倍数进行标记

```rust
//假设区间范围为1e+5
fn E_sieve(n:i32)->Vec<i32>{
    // 标记数组
    let mut res:Vec<i32>=vec![0;1e+5];
    for i in 2..=n{
        if res[i]==0{
            // 对每个素数都要把其所有的倍数都进行标记，看起来时间复杂度很大，但其实很多元素都被标记后
            // 后期if判断语句基本不会进入
            let j=i*i;
            while j<=n{
                res[j]==1;
                j+=i;
            }
        }
    }
}
```

> (更快的方法)欧拉筛 (因为在埃氏筛中一个合数有可能会被多个因子多次标记，这样就造成了时间浪费，比如12会被2筛一次，被3筛一次所以欧式筛的核心思想就是减少这些时间浪费，使得被标记的元素尽量是被其最小质因子标记，12只被2标记)

```rust
```







## 并查集

并查集是一种用于管理元素所属集合的数据结构，实现为一个森林，其中每棵树表示一个集合，树中的节点表示对应集合中的元素

并查集支持两种操作

- 合并(union)：合并两个元素所在的集合 
- 查询(find)：查询某个元素所属集合（查询根节点）,并判断两个元素是否属于同一集合



> 对于最初的元素，每个元素的根节点都是自己，所以一个长度为n的数组其中每个下表所存储位置的值是本身



> 查询

```rust
// 因为只是对向量中的数进行查询，所以使用引用即可，也不消耗所有权
fn find(parents:&Vec<usize>,value:usize)->usize{
    if parents[value]==value{
        return value;
    }
    // 这里的parents 本身已经是 &Vec<i32> 类型所以不需要作任何的操作 直接传入即可
    // 这里使用clone 不消耗向量中值的所有权
    find(parents,parents[value].clone())
}


// find 的路径压缩算法
fn find(parents:&mut Vec<usize>,value:usize)->usize{
    if parents[value]==value{
        return value;
    }
    // 这一步是为了把所有节点直接与根节点相连，优化后续查找的时间复杂度，对当前查找并没有优化
    parents[value]=find(parents,parents[value].clone());
    return parents;
}
```

> 合并

```rust
// 实际意义是把一个集合的根节点连到另一个集合的根节点上去
pub fn union(parents:&mut Vec<usize>,x:usize,y:usize){
    parents[find[x]]=find[y];
}
```



## 线段树







## 回溯算法



No.77 组合

> 给定两个整数 `n` 和 `k`，返回范围 `[1, n]` 中所有可能的 `k` 个数的组合。
>
> 你可以按 **任何顺序** 返回答案。
>
> **示例 1：**
>
> ```
> 输入：n = 4, k = 2
> 输出：
> [
>   [2,4],
>   [3,4],
>   [2,3],
>   [1,2],
>   [1,3],
>   [1,4],
> ]
> ```
>
> **示例 2：**
>
> ```
> 输入：n = 1, k = 1
> 输出：[[1]]
> ```



```rust
impl Solution {
    pub fn combine(n: i32, k: i32) -> Vec<Vec<i32>> {
        let mut res:Vec<Vec<i32>>=Vec::new();
        let mut path:Vec<i32>=Vec::new();
        dfs(n,&mut path,k as usize,&mut res);
        res
    }
}

pub fn dfs(value:i32,path:&mut Vec<i32>,len:usize,res:&mut Vec<Vec<i32>>){
    if path.len()==len{
        res.push(path.clone());
        return;
    }
    for i in (1..=value).rev(){
        path.push(i);
        dfs(i-1,path,len,res);
        path.pop();
    }
}
```

