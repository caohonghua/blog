---
permalink: /database/ranking/
---

# 排名函数
在查询数据时，可以对数据进行排名操作，主要分为一下几种：
* row_number() 行号
* rank() 跳跃排名
* dense_rank() 连续排名

#### 注：MySQL 排名函数是版本8才有的，之前的版本需要使用变量模式； 在关联查询中采用变量模式的排名，需要先关联查询，得到结果后，再使用变量模式排名得到最终结果。


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


### row_number()
```
MySQL Version : 8.*
select name,chinese,row_number() over(order by chinese desc,name asc) ranking from score;

MySQL Version: 5.*
select name,chinese, @rank:=@rank+1 ranking from score,(select @rank:=0 from dual) r order by chinese desc,name asc;
```
### 数据结果
| id | name   | chinese | math | english |
|----|--------|---------|------|---------|
| 小明       |      95 |       1 |
| 小蓝       |      94 |       2 |
| 哆啦A梦    |      90 |       3 |
| 小刚       |      90 |       4 |
| 小紫       |      90 |       5 |
| 小红       |      90 |       6 |
| 小林       |      88 |       7 |

### rank()
```
MySQL Version: 8.*
select name, chinese ,math,english,rank() over(partition by chinese order by math desc) ranking from score;

MySQL Version: 5.*
select name,chinese,math,english,
 if(@rank_chinese = chinese, @rank_counter:= @rank_counter+1 ,@rank_counter:=1) temp, if(@rank_chinese = chinese, if(@rank_math = math, @cur_rank, @cur_rank:=@rank_counter), @cur_rank:=1) ranking,  @rank_chinese := chinese, @rank_math :=math from score, (select @rank_chinese:=NULL,@rank_math:=NULL,@rank_counter:=1,@cur_rank:=0 from dual) r order by chinese, math desc;
```

### 数据结果

 name   | chinese | math | english | ranking|
--------|---------|------|---------|--------|
| 小林       |      88 |   95 |      95 |       1 |
| 小红       |      90 |   99 |      90 |       1 |
| 小紫       |      90 |   99 |      90 |       1 |
| 哆啦A梦    |      90 |   99 |     100 |       1 |
| 小刚       |      90 |   95 |      90 |       4 |
| 小蓝       |      94 |  100 |      92 |       1 |
| 小明       |      95 |   98 |     100 |       1 |


### dense_rank()
```
MySQL Version: 8.*
 select name, chinese,math,english, dense_rank() over(partition by chinese order by chinese desc, math desc ) ranking  from score;

 MySQL Version: 5.*
 select name ,chinese,math,english, if(@rank_chinese = chinese, if(@rank_math = math,@cur_rank,@cur_rank:=@cur_rank+1),@cur_rank:=1) ranking, @rank_chinese := chinese, @rank_math := math from score,(select @cur_rank:=0,@rank_chinese:=NULL,@rank_math:=NULL from dual) r order by chinese, math desc;
```
### 数据结果

 name   | chinese | math | english | ranking|
--------|---------|------|---------|--------|
| 小林       |      88 |   95 |      95 |       1 |
| 小红       |      90 |   99 |      90 |       1 |
| 小紫       |      90 |   99 |      90 |       1 |
| 哆啦A梦    |      90 |   99 |     100 |       1 |
| 小刚       |      90 |   95 |      90 |       2 |
| 小蓝       |      94 |  100 |      92 |       1 |
| 小明       |      95 |   98 |     100 |       1 |