
# 扁平转Tree  Tree 平铺

## 扁平转Tree适用范围 ：
在服务端给的树形结构无法满足业务要求时，又无法使服务器进行更改,直接拿原始数据
前端对原始数据进行整理 转为符合自己业务要求的数据结构

## Tree 平铺适用范围 ：
当只有树形结构时，将树形结构转为一维数据，再对一维数据进行整理，转为符合自己预期的数据结构


### 遇到的问题
扁平转Tree 循环之后 如何找到父节点并把数据加入父节点中
如果有多层嵌套要怎么办 父与子的关系应该怎么表达


### 解决方案1 
1. 声名一个 数组为 treeSource 为一维扁平数据 为源数据
1. 声名一个 数组为 result 存放最后转化后的Tree
2. 声名一个 对象为itemMap 存放 treeSource 中的每个节点
4. 循环 treeSource 并命名每个节点为node 
5. 声名变量 id pin 为当前 node节点的id pid 
6. 判断itemMap中是否有 当前节点 id 为key的数据 ，没有便添加 id 为 key {chidlren:[]} 为value的 对象
7. 添加完毕之后，把当前的node数据itemMap中id为key的数据合并起来
8. 合并完毕之后 取出当前itemMap中 id 为 key的数据

9. 判断当前node节点的pid是否为0 如果为 0 说明为根节点 便把itemMap中当前id为key的值push到result中
10. 如果当前节点的pid不为0 说明为其他子节点 
11. 那么便在 itemMap中找到 以 当前node节点 pid 为key的值并把这个值的children push 当前itemMap中以当前node节点id为key的值

12. 计算完成

#### 核心难点

1. 把源数据节点循环 以 每个节点 id 为 key {children:[]} 为value 存入到itemMap对象中 并合并

2. 每次迭代 判断 pid 是否为 0 

   2.1 如果为0 itemMap中当前 id 的数据放入到 result中
   2.2 如果不为0 取出itemMap中 pid 为 key 的数据 的children 并把children push itemMap以当前id的数据

```js
  { id: 2, name: "部门2", pid: 1 },
```

3. 如果当前节点的 pid 为 1  那么在itemMap中找到 当前pid的数据 的children    itemMap[pid]["children"]
4. 把 当前itemMap中以当前 id 为 key 的数据取出来  push 到 itemMap[pid]["children"] 中


### 解决方案2 







### 源数据
```javascript

    let treeSource = [
        { id: 1, name: "部门1", pid: 0 },
        { id: 2, name: "部门2", pid: 1 },
        { id: 3, name: "部门3", pid: 1 },
        { id: 4, name: "部门4", pid: 3 },
        { id: 5, name: "部门5", pid: 4 },
    ];

```


### 最后的结果

```javascript
    [
        {
            "id": 1,
            "name": "部门1",
            "pid": 0,
            "children": [
                {
                    "id": 2,
                    "name": "部门2",
                    "pid": 1,
                    "children": []
                },
                {
                    "id": 3,
                    "name": "部门3",
                    "pid": 1,
                    "children": [
                        {
                            "id": 4,
                            "name": "部门4",
                            "pid": 3,
                            "children": [
                                {
                                    "id": 5,
                                    "name": "部门5",
                                    "pid": 4,
                                    "children": []
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]


```








