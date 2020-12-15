---
permalink: /database/rowtocolumn/
---

# 行转列
* Oracle ： listagg(字段,'分隔符') within group([order by 排序字段 asc/desc]) 
* MySQL : group_concat([distinct] 字段 order by [order by 排序字段 asc/desc][separator '分隔符']) ... group by 


### 数据表
```
CREATE TABLE `score` (
  `id` int NOT NULL AUTO_INCREMENT COMMENT 'id',
  `name` text COMMENT '姓名',
  `chinese` float DEFAULT NULL COMMENT '语文',
  `math` float DEFAULT NULL COMMENT '数学',
  `english` float DEFAULT NULL COMMENT '英语',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8 ;

insert into score(name,chinese,math,english) values  ('小明',95,98,100), ('小红',90,99,85), ('小刚',90,95,90), ('小林',88,95,95), ('小蓝',94,100,92),('小紫',90,99,90),('哆啦A梦',90,99,100);
```

### 数据显示

| id | name   | chinese | math | english |
|----|--------|---------|------|---------|
|  1 | 小明   |      95 |   98 |     100 |
|  2 | 小红   |      90 |   99 |      85 |
|  3 | 小刚   |      90 |   95 |      90 |
|  4 | 小林   |      88 |   95 |      95 |
|  5 | 小蓝   |      94 |  100 |      92 |
|  6 | 小紫   |      90 |   99 |      90 |
|  7 | 哆啦A梦    |      90 |   99 |     100 |

### listagg()
```
select chinese,listagg(name ',') within group(order by name) names from score; 
```

### group_concat()
```
select chinese , group_concat(name order by name) names from score group by chinese;
```


### 结果显示
|---------|----------------------|
| chinese | names                |
|---------|----------------------|
|      88 | 小林                  |
|      90 | 小红,小刚,小紫,哆啦A梦  |
|      94 | 小蓝                 |
|      95 | 小明                  |

