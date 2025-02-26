# openGSQL (open Graph-Relation Structured Query Language)
## 背景
### 关系代数
关系代数的运算对象是关系，运算结果也是关系。关系代数中用到的运算符主要有以下的类型：
1. 集合运算符
    - 并 $\cup$
    - 交 $\cap$
    - 差 $-$
    - 笛卡尔积 $\times$
2. 专门的关系运算符
    - 选取 $\sigma$
    - 投影 $\prod$
    - 除 $\div$
    - 自然连接 $\bowtie$
    - $\theta$连接 $\bowtie_{X \theta Y}$
3. 算术比较运算符
    - 大于
    - 小于
    - 大于等于
    - 小于等于
    - 等于
    - 不等于
4. 逻辑运算符
    - 与 $\lor$
    - 或 $\land$
    - 非
#### 运算定义
##### 相容
给定两个关系$R$、$S$ ，如果他们满足：
1. 具有相同的列数 $n$
2. $R$ 中的第 $i$ 个属性和 $S$ 中的第 $i$ 个属性必须来自同一个域
   那么我们就称 $S$ 和 $S$ 是相容的。

##### 并 Union
$$ R \cup S = \{t|t \in R \lor t \in S\} $$

##### 差 Difference
$$ R - S = \{ t | t\in R \land t \notin S \} $$

##### 交 Intersection
$$ R \cap S  = \{ t | t \in R \land t \in S \} $$

##### 广义笛卡尔积 Extended Cartesian Product
$$ R \times S = \{ t_r \sim t_s | t_r \in R \land t_s \in S \} $$

#### 专门的关系运算定义
传统的集合运算，只是从行的角度进行，而要灵活地实现关系数据库多样的查询操作，必须引入专门的关系运算。在介绍专门的关系运算之前，为了叙述上的方便，先引入几个概念：
- 设关系模式为$R(A_1,A_2​,…,A_n​)$，它的一个关系为$R$，$t\in R$表示$t$是$R$的一个元组，那么$t[A_i​]$表示元组$t$相对于属性$A_i$​的一个分量；
- 给定一个关系$R(X,Z)$，$X$和$Z$为属性组，定义当$t[X]=x$时，$x$在$R$中的像集Image Set为$Z_x​=\{t[Z]|t\in R,t[X]=x\}$，它表示的是$R$中属性组$X$上值为$x$的那些元组在$Z$分量上的集合。

##### 选取Selection
选取运算是单目运算，它根据一定的条件从关系$R$中选择若干个元组，组成一个新的关系。选取操作记作：
$$ \sigma_F(R) = \{ t | t \in R \land F(t) = True \} $$
其中$\sigma$为选取运算符，$F$是选取的条件。$F$是由运算对象(属性名、常数、简单函数)、算术比较运算符(＞、≥、＜、=、≠)和逻辑运算符(与、或、非)连接起来的逻辑表达式，其结果是逻辑值True或False，所以我们对于选取运算进行总结：它从关系$R$中选取那些使得逻辑表达式$F$为真的元组，是从行的角度进行的运算。

##### 投影Projection
投影运算也是单目运算，关系$R$上的投影是从$R$中选择出若干属性列，组成新的关系，即对关系$R$在垂直方向上进行运算，从左到右按照指定的若干属性及顺序(意味着我们可以改变属性列的顺序，实际上关系中的属性列是可以交换位置的)取出相应列，并且要删除重复的元组。投影运算记作：
$$ \prod_A(R) = \{ t[A] | t \in R \} $$

##### $\theta$连接 $\theta$ Join
$\theta$连接运算是一个二元运算，其效果是从两个关系$R$和$S$的笛卡尔积中选取满足连接条件的元组，而后组成新的关系。设两个关系$R$和$S$，它们的属性列数分别为$n$和$m$，其中$R$中的属性可以进一步分解为属性集$Z$和$X$，即$R=(Z，X)$，关系$S$可以进一步分解为属性集$W$和$Y$，即$S=(W，Y)$。如果我们认定$X$和$Y$是连接属性(需要$X$和$Y$的属性列数相等)，那么关系$R$和$S$在连接属性$X$和$Y$上的$\theta$连接，就是在$R$和$S$的笛卡尔积中选择那些$X$属性集上的分量与$Y$属性集上的分量满足$\theta$比较条件的那些元组。新关系的列数为$(n+m)$，即两个关系的列数和，记作：


## 图-关系代数
### 图定义
定义属性关系图
$$ \mathcal{G}(\mathbb{V},\mathbb{E},\mathbb{T}) = \{R | R \in \mathbb{V} \lor R \in \mathbb{E} \lor R \in \mathbb{O} \} $$
简记为$\mathcal{G}$，其中 $\mathbb{V} = \{V_1,V_2,V_3,...,V_n\}$ 为顶点关系的集合，$\mathbb{E} = \{E_1,E_2, E_3 ,...E_m\}$ 为边关系的集合，$\mathbb{O} = \{O_1,O_2,O_3,...O_i\}$ 为普通关系集合；
其中顶点关系定义为：设顶点关系$V$的模式为$V(id,P_1,P_2,...P_k)$,其属性$id$具有图全局唯一性，即两个顶点关系元组$v,w$,如果$v[id] = w[id]$ 则 $v = w$。
其中边关系定义为：设边关系$E$的模式为$E(src,dst,P_1,P2,...P_k)$，其属性$src,dst$为图中某两个顶点关系$id$，其中的元组$e$代表$id$为$src$的顶点元组指向$id$为$dst$的顶点元组的边。

#### 图关系的类型
定义关系$R$的类型为 $T^R$ , 如果两个关系 $R,S$ 满足：
$$ T^R = T^S $$
则 $R$ 与 $S$ 相容。

##### 图模式
$$ T^\mathcal{G} = \{ T^{V_1},T^{V_2},...T^{V_n},T^{E_1},T^{E_2},...T^{E_m},T^{O_1},T^{O_2},...T^{O_i} \} $$

所以图$\mathcal{G}$也可以记为

| $T^{V_1}$ | $T^{V_2}$ | ... | $T^{V_n}$ | $T^{E_1}$ | $T^{E_2}$ | ... | $T^{E_m}$ | $T^{O_1}$ |$T^{O_2}$|...|$T^{O_i}$ |
| -- | -- | -- | -- | -- |  -- |  -- |  -- |   -- |   -- |   -- |   -- |
| $V_1$ | $V_2$ | ... | $V_n$ | $E_1$ | $E_2$ | ... | $E_m$ | $O_1$ | $O_2$ | ... | $O_i$ |

##### 复合类型
###### Union type
定义类型 $T^R | T^S$, 如果 $T^X = T^R |  T^S$ ，则 $ \{ t | t \in T \land (t \in R \lor t \in S) \} $
###### List type
$List[T]$ 为类型为$T$的关系的列表


### 代数操作
#### 图集合运算
##### 定义
$$ t \in\in \mathcal{G}(\mathbb{V}, \mathbb{E}, \mathbb{R}) $$
when
$$ \{ t | t \in R , R \in \mathbb{V} \lor R \in \mathbb{E} \lor R \in \mathbb{R} \} $$
##### 并
$$ \mathcal{G}_1 \cup \mathcal{G}_2 = \{ t | t \in\in \mathcal{G}_1 \lor t \in\in \mathcal{G}_2 \} $$

##### 交
$$ \mathcal{G}_1 \cap \mathcal{G}_2 = \{ t | t \in\in \mathcal{G}_1 \land t \in\in \mathcal{G}_2 \}   $$

##### 差
$$  \mathcal{G}_1 - \mathcal{G}_2 = \{ t | t \in\in \mathcal{G}_1 \land t \notin\notin \mathcal{G}_2 \}  $$

##### right
$$ right(\mathcal{G}_1,\mathcal{G}_2 ) = \mathcal{G}_2 $$

##### left
$$ left(\mathcal{G}_1,\mathcal{G}_2 ) = \mathcal{G}_1 $$

##### Join
$$  $$

#### 图专有运算
##### 投影
$$ \prod_A \mathcal{G} (\mathbb{V}, \mathbb{E}, \mathbb{R} ) = \{ \mathbb{V}_A, \mathbb{E}_A, \mathbb{R}_A | V_T  \}$$
##### 选取
$$  \sigma_P(\mathcal{G}) = \{t | t \in\in \mathcal{G} \land P(t) = True \} $$

##### 结构谓词

$$ (R)-[E]\to[S] = True  $$
when
$$  \{t,e,s | t \in R , e \in E , s \in S, t[id] = e[src] \land e[dst] = s[id] \}  $$


### 示例
#### create database

```sql
create database ent_graph;
```

#### use database

```sql
use ent_graph;
```

#### create vertex
```sql
create vertex person (
    name varchar(100) not null default '',
    age int 
) with space 1;

create vertex company (
    name varchar(500) ,
    industry_code int ,
    credit_code varchar(200),
    reg_number varchar(100)
);

create vertex goverment (
    name varchar(500),
    uuid varchar(200)
);
```

#### create edge
```sql
create edge work_in (
    start_date date ,
    end_date date ,
    role varchar(50)
) on person to company or person to goverment ;

create edge friend (
    start_date date
) on person connect person;
```

#### create attach table
```sql
create table person_extra (
    weight double,
    address varchar(500)
) attach person;
```

#### create table
```sql
create table test (
    hello varchar(50) 
);
```

#### show

```sql
show databases;
show vertices;
show edges;
show tables;
SHOW COLUMNS FROM person;
```



### query example


```sql
select * from test;
select * from ent_graph.test;

select * from ent_graph.person;
select name, age from (select p from ent_graph match (p:person)) t;

select * from ent_graph;

select p,f,c from ent_graph
match (p:person)-[f:friend]->(pp:person) and (pp)-[w:work_in]->(c:company | goverment)
where c.name in ['', '', ''];


with recursive loop_group as (
    select p,c,g from ent_graph match (p:person), (c:company), [g:guar]
    except 
    select p,c,g uinon gr as g from loop_group match (p:person)-[g:guar]-(), (c:company)-[gr:guar]-() 
    where p.in_degree = 0 or p.out_degree = 0 , c.in_degree = 0 or c.out_degree = 0 
)
select * from loop_group;

with recursive dfs as (
    select array(inc) as step from ent_graph match (inc:person) where inc.name = 'tom'
    right 
    select dfs.step :: new_inc as setp from ent_graph join dfs
        on dfs.step(-1) = ent_graph.person match (dfs.step(-1))-[]->(new_inc) and new_inc not in step
)


select r,s from G match (r:Researcher)-([sp:SUPERVISES|RULE]->(s:Student)){3,6}->() 
    where r.name = '' and (r.out.SUPERVISES between (3,5) or r.out.RULE > 1) ,
     sp.start_date > '' 

```