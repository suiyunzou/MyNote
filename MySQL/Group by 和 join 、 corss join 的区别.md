<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">假设我们有一个 </font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">sales</font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"> 表,包含 </font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">product_id</font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">, </font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">category</font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">, </font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">sale_date</font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">, 和 </font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">amount</font>`<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"> 字段。</font>

## <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">Group by使用的5种情况</font>
1. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">基本分组:显示每个类别的总销售额。</font>

```plain
SELECT category, SUM(amount) as total_sales
FROM sales
GROUP BY category;
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

2. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">多列分组:这会按类别和年份分组,显示每个类别每年的销售额。</font>

```plain
SELECT category, YEAR(sale_date) as year, SUM(amount) as total_sales
FROM sales
GROUP BY category, YEAR(sale_date);
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

3. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">使用 HAVING 子句:HAVING 用于过滤分组后的结果,类似于 WHERE 对个别行的过滤。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">这会只显示总销售额超过 10000 的类别。</font>

```plain
SELECT category, SUM(amount) as total_sales
FROM sales
GROUP BY category
HAVING total_sales > 10000;
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

4. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">与 ORDER BY 结合:这会显示每个类别的销售次数,并按销售次数降序排列。</font>

```plain
SELECT category, COUNT(*) as sale_count
FROM sales
GROUP BY category
ORDER BY sale_count DESC;
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

5. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">使用 WITH ROLLUP:WITH ROLLUP 提供额外的汇总行。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">这会为每个类别和年份组合提供小计,以及整体总计。</font>

```plain
SELECT category, YEAR(sale_date) as year, SUM(amount) as total_sales
FROM sales
GROUP BY category, YEAR(sale_date) WITH ROLLUP;
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

## <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">a join b、a corss join b、 a,b的区别</font>
1. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">使用 CROSS JOIN 关键字：</font>

```plain
SELECT * FROM Fruits CROSS JOIN Colors;
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">这是最标准和明确的语法。在 MySQL InnoDB 中，这种写法清晰地表明了您想要执行一个笛卡尔积操作。它的优点是代码可读性强，意图明确，并且符合 SQL 标准。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

2. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">使用 JOIN 而不指定类型：</font>

```plain
SELECT * FROM Fruits JOIN Colors;
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">在 MySQL 中，如果使用 JOIN 而不指定类型（如 INNER JOIN 或 LEFT JOIN 等），并且没有 ON 或 USING 子句，MySQL 会将其视为 CROSS JOIN。这种语法更简洁，但可能会让不熟悉的读者感到困惑，因为通常 JOIN 会期望有一个连接条件。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);"></font>

3. <font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">使用逗号分隔表名：</font>

```plain
SELECT * FROM Fruits, Colors;
```

<font style="color:rgb(0, 0, 0);background-color:rgb(247, 247, 247);">这是一种较老的语法，在 MySQL 中仍然有效。当在 FROM 子句中用逗号分隔多个表，且没有 WHERE 子句指定连接条件时，MySQL 会将其解释为 CROSS JOIN。这种语法简单，但可能不如 CROSS JOIN 关键字清晰。</font>

<font style="background-color:rgb(247, 247, 247);"></font>

