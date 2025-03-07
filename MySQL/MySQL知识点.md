#  SELECT语句

```sql
select 
    column1[,column2,...|聚合函数|表达式]
    [distinct] 												#去重
from 
    table_name 	[as]alias							#表名[，可选别名]
    [JOIN 类型]table_name2 
    on 条件														#表连接
where 
    条件表达式													#行级过滤
    #比较运算符：<、>、=、!=、<>、>=、<=
    #逻辑运算符：and、or、not
    #范围：not in、in、between and
    #模糊匹配：like、not like(_单个字符、%多个字符)
    #空值：is null、is not null
group by 
    column_name1[,column_name2，...]  #分组
having
    分组条件														#组级别过滤
order by 
    column_name1 [asc|desc] [,column_name2 [asc|desc]	, ...]		#排序
limit offset，row_count 							#分页，offset表示起始偏移量(从0计数，0即第一条记录)，
                                      #			 row_count表示读取的记录数
```

# select补充点：

1. 执行顺序：

```markdown
from、join  、on 、where、group by、聚合函数、having、select、窗口函数、order by、limit；

1. FROM
2. JOIN
3. ON
4. WHERE
5. GROUP BY
6. 聚合函数
7. HAVING
8. SELECT
   - 窗口函数（在SELECT阶段最后执行）
9. ORDER BY
10. LIMIT
-- 案例：
SELECT 
    department,
    name,
    salary,
    -- 聚合函数
    AVG(salary) as dept_avg,
    -- 窗口函数
    ROW_NUMBER() OVER(PARTITION BY department 
                      ORDER BY salary DESC) as dept_rank,
    -- 引用前面的窗口函数结果
    CASE 
        WHEN ROW_NUMBER() OVER(PARTITION BY department 
                               ORDER BY salary DESC) <= 3 
        THEN 'Top 3' 
        ELSE 'Others' 
    END as rank_category
FROM employees e
JOIN departments d 
    ON e.dept_id = d.id
WHERE status = 'active'
GROUP BY department, name, salary
HAVING AVG(salary) > 5000
ORDER BY department, salary DESC
LIMIT 10;
```

<details class="lake-collapse"><summary id="ub749d383"><span class="ne-text">案例的执行顺序：</span></summary><ol class="ne-ol" style="margin: 0; padding-left: 23px"><li id="u864f45d9" data-lake-index-type="0"><span class="ne-text">from employees e</span></li><li id="u243a9a5f" data-lake-index-type="0"><span class="ne-text">join departments d 、</span></li><li id="u790bec4b" data-lake-index-type="0"><span class="ne-text">on   e.dept_id = d.id</span></li><li id="uce53cd0c" data-lake-index-type="0"><span class="ne-text">where status = 'active'</span></li><li id="ud2783c45" data-lake-index-type="0"><span class="ne-text">GROUP BY department, name, salary</span></li><li id="u106cc75b" data-lake-index-type="0"><span class="ne-text"> AVG(salary)  as dept_avg</span></li><li id="ue496406d" data-lake-index-type="0"><span class="ne-text">HAVING AVG(salary) &gt; 5000</span></li><li id="u57178340" data-lake-index-type="0"><span class="ne-text">select部分：</span></li></ol><pre data-language="plsql" id="hpvK3" class="ne-codeblock language-plsql" style="border: 1px solid #e8e8e8; border-radius: 2px; background: #f9f9f9; padding: 16px; font-size: 13px; color: #595959"><code>SELECT 
    department,
    name,
    salary,
    -- 聚合函数
    AVG(salary) as dept_avg,
    -- 窗口函数
    ROW_NUMBER() OVER(PARTITION BY department 
                      ORDER BY salary DESC) as dept_rank,
    -- 引用前面的窗口函数结果
    CASE 
        WHEN ROW_NUMBER() OVER(PARTITION BY department 
                               ORDER BY salary DESC) &lt;= 3 
        THEN 'Top 3' 
        ELSE 'Others' 
    END as rank_category</code></pre><ol start="9" class="ne-ol" style="margin: 0; padding-left: 23px"><li id="ued8b09c6" data-lake-index-type="0"><span class="ne-text">ORDER BY department, salary DESC</span></li><li id="u2f352c22" data-lake-index-type="0"><span class="ne-text">LIMIT 10;</span></li></ol></details>



1. join的类型：

```markdown
 table1 cross join table2 		当没有连接条件时(on)等价cross join =join ，
 table1 inner join table2 	 		inner join =join ，
 table1 left join table2  		左外连接，表示table1、table2都有的与table2独有的
 table1 right join table2  	右外连接
 table1 natural join table2 	自然连接，当有相同字段时自动匹配，但要慎用
```

1. 常用的聚合函数

```markdown
-- 基础聚合函数
COUNT()   -- 计数
SUM()     -- 求和
AVG()     -- 平均值
MAX()     -- 最大值
MIN()     -- 最小值

-- 示例
SELECT 
    department,
    COUNT(*) as 员工数,
    AVG(salary) as 平均工资,
    MAX(salary) as 最高工资,
    MIN(salary) as 最低工资,
    SUM(salary) as 工资总和
FROM employees
GROUP BY department;
```

1. 窗口函数

```markdown
1. 排名函数
ROW_NUMBER()   -- 连续排名 1,2,3,4，相同条件时有不同排名
RANK()         -- 跳跃排名 1,1,3,4
DENSE_RANK()   -- 连续排名 1,1,2,3，	相同排名时有相同排名

-- 示例：按工资排名
SELECT 
name,
salary,
ROW_NUMBER() OVER(ORDER BY salary DESC) as 连续排名,
RANK() OVER(ORDER BY salary DESC) as 跳跃排名,
DENSE_RANK() OVER(ORDER BY salary DESC) as 连续排名2
FROM employees;

2. 分区函数
-- 分组排名
ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC)

-- 示例：各部门工资排名
SELECT 
department,
name,
salary,
ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC) as dept_rank
FROM employees;
```

1. 