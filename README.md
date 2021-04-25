# composer require mdao/query_orm


# 查询表达式
表达式`不分大小写`，支持的查询表达式有下面几种，分别表示的含义是：

| 表达式                         | 描述             |
| ------------------------------ | ---------------- |
| filter[field[eq]]=1            | 等于             |
| filter[field[neq]]=1           | 不等于           |
| filter[field[gt]]=1            | 大于             |
| filter[field[egt]]=1           | 大于等于         |
| filter[field[lt]]=1            | 小于             |
| filter[field[elt]]=1           | 小于等于         |
| filter[field[like]]=1          | 模糊查询         |
| filter[field[[not] in]]=1      | （不在）in 查询  |
| filter[field[[not] between]]=1 | （不在）区间查询 |

## 表达式查询的用法示例如下：

eq ：等于（=）
---
例如：
```
url?filter[id[eq]]=100 
或者
url?filter[id]=100 
```
服务端会解析成
```php
where('id',100);
```
表示的查询条件就是 id = 100

neq ：不等于（<>）
---
例如：
```
url?filter[id[neq]]=100 
```
服务端会解析成
```php
where('id','<>',100);
```
表示的查询条件就是 id != 100

gt ：大于（>）
---
例如：
```
url?filter[id[gt]]=100 
```
服务端会解析成
```php
where('id','>',100);
```
表示的查询条件就是 id > 100

egt ：大于等于（>=）
---
例如：
```
url?filter[id[egt]]=100 
```
服务端会解析成
```php
where('id','>=',100);
```
表示的查询条件就是 id >= 100

lt ：小于（<）
---
例如：
```
url?filter[id[lt]]=100 
```
服务端会解析成
```php
where('id','<',100);
```
表示的查询条件就是 id < 100

elt ：小于等于（<=）
---
例如：
```
url?filter[id[elt]]=100 
```
服务端会解析成
```php
where('id','<=',100);
```
表示的查询条件就是 id <= 100

like ：同sql的LIKE
---
例如：
```
url?filter[id[like]]=张三% 
```
服务端会解析成
```php
where('id','like','张三%');
```

in ：查询 id为1,2,3 的数据
---
例如：
```
url?filter[id[in]]=1,2,3 
```
服务端会解析成
```php
where('id','in',['1','2','3']);
```
not in ：查询 id不等于1,2,3 的数据
---
例如：
```
url?filter[id[not in]]=1,2,3 
```
服务端会解析成
```php
where('id','not in',['1','2','3']);
```

between ：查询 id为1到8 的数据
---
例如：
```
url?filter[id[between]]=1,8 
```
服务端会解析成
```php
where('id','between','1,8');
```
not between ：查询 id 不在 1,8 的数据
---
例如：
```
url?filter[id[not between]]=1,8
```
服务端会解析成
```php
where('id','not between','1,8');
```
多字段，多条件组合使用使用
```
url?filter[type[eq]]=1&filter[age[lt]]=50&filter[sex[neq]]=2
```
服务端会解析成
```php
where([
['type','=',1],
['age','<',50],
['sex','<>',2],
]);
```
表示的查询条件是 type=1 并且 age<50 并且 sex!=2


   'page' => 1,
    'select' => 'a,b,d',
    // 'page_size' => 15,
# 分页

| 参数名                         | 描述             |
| ------------------------------ | ---------------- |
| page            | 页码，从1开始 |
| page_size           | 每页几条数据         |

用法示例如下：
```shell script
url?page=1&page_size=15
```

# 排序
| 参数名                         | 描述             |
| ------------------------------ | ---------------- |
| order_by            | 排序字段 |
| sorted_by           | 排序方式 默认就是升序排列 |
用法示例如下：
```shell script
url?order_by=id&sorted_by=desc
```

