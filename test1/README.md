# 作业1

姓名：陈智明

学号：201810414108

班级：软件工程1班

### 实验目的

分析SQL执行计划，执行SQL语句的优化指导。理解分析SQL语句的执行计划的重要作用。

### 实验内容

- 对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
- 首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
- 设计自己的查询语句，并作相应的分析，查询语句不能太简单。

### 查询1

```sql
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT','Sales')
GROUP BY d.department_name;
```

![](https://github.com/chen-shrewd/oracle/blob/master/test1/chaxun1.png)

### 查询

```sql
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
FROM hr.departments d,hr.employees e
WHERE d.department_id = e.department_id
GROUP BY d.department_name
HAVING d.department_name in ('IT','Sales');
```

![](https://github.com/chen-shrewd/oracle/blob/master/test1/chaxun2.png)

##### 通过分析判断查询2是最优的

##### SQL优化指导

![](https://github.com/chen-shrewd/oracle/blob/master/test1/youhua2.png)

##### 自己设计的SQL语句：查询工资大于10000的员工姓名

```sql
SELECT FIRST_NAME,LAST_NAME,sum(SALARY)
FROM hr.employees 
GROUP BY SALARY, FIRST_NAME, LAST_NAME
HAVING SALARY > 10000
```

##### SQL优化指导

![](https://github.com/chen-shrewd/oracle/blob/master/test1/youhua3.png)