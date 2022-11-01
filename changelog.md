# 版本变更记录

`*` 表示需要升级对应版本的 IDEA 插件

### 0.11.10

1. 优化了数据库结构比对异常 `SqlExCheckException` 的 `message`, 让人更快发现异常原因.
2. 提供了缓存机制, 优化了 Maven/Gradle 的构建速度.

### 0.11.9

1. (fix) 修复 `is null` 常量折叠优化中的表达式判断问题, 该问题会在大写 SQL 语句时出现.

### 0.11.8 \*

1. 兼容 `IDEA 2022.3 EAP`
2. (fix) 修复 `查看生成的Java文件` 功能

### 0.11.7

1. 优化了原生库的打包方式, 将各个平台的原生库分离打包, 减少依赖下载/分析过程中的错误

### 0.11.4 \*

1. (fix) 修复 数据库名替换 在 `with` 子句中不起作用的问题

### 0.11.3 \*

1. (fix) 优化 SQL 解析器, 修复 `limit` 错误转化的问题
2. (fix) 修复 `col in (:var)` 可能会错误认定为单行结果的问题

### 0.11.2

1. 优化 FFI 调用, 弃用 Gson, 使用 jackson 来做 FFI 调用数据的序列化
2. (fix) 修复 0.11.0 版本新增 `外部 Schema` 功能时, 引入的 SQL 语句分析 BUG, 该 BUG 会造成 `is null 折叠` 和 `in 参数展开` 分析错误

### 0.11.1

1. 迁移回调 SQL 支持直接从 classpath/文件/流等位置读取
2. (fix) 优化配置文件解析, 弃用 kaml 库(其会造成 kotlin 版本的兼容性问题)

### 0.11.0 \*

1. 添加了 `外部 Schema` 引入的支持
2. (fix) 修复 `column = (subquery)` 的解析问题
3. 添加了 `迁移回调` 的功能, 能在指定版本迁移前后执行 java 代码
4. 优化了迁移任务, 能正常记录下迁移的进度

### 0.10.27 \*

1. 添加单 `alter` 语句变更多个列的功能

### 0.10.26

1. (fix) 修复了 `Blob (二进制)类型` 的获取, 当前版本除了 sqlm 中不能使用 `byte[]` 作为参数外, 其他 API 对于二进制的处理均已正常
2. 加入了新的 `RawSQLExecutor API`, 提供了除 sqlm 和 单实体 API 外第三种执行 SQL 的方法. 通过 `factory.getRawSQLExecutor()` 获取到执行器实例

### 0.10.25

1. (fix) 修复 Spring 异常翻译的 bug, 其可能会造成异常湮没, 变成 `NullPointerException`

### 0.10.24

1. (fix) 修复了 gradle 插件不自动配置 test 源码 apt 的问题

### 0.10.23 \*

1. (fix) 点击刷新索引的按钮时, 会自动保存当前的文档
2. 修改创建时候的文件模版, 去掉了不必要的头部信息
3. 优化生成代码中的 javadoc, 防止警告
4. (fix) 修复 gradle 插件对于多源码目录多支持问题

### 0.10.22 \*

1. 优化了 sqlm 文件的语法高亮, 现在能根据语法元素的类型(方法名/参数/参数类型等)来显示不同的颜色
2. (fix) 修复了 gradle 中自动配置 annotationProcessor 的 bug

### 0.10.21

1. (fix) 修复了 gradle 插件的依赖检查 bug, 现在不再强制检查间接依赖

### 0.10.20 \*

1. lambda 作为参数的 `where` 方法已经**弃用**, kotlin 拓展的 filter 保持
2. sqlm 中的 insert 语句现在能返回自动生成的列
3. 优化了 annotationProcessor 的架构, 当 annotationProcessor 意外被禁用时保证编译不通过

### 0.10.19

1. 优化了 Gradle 插件的实现, 现在项目依赖可以不用加版本号了, 插件会自动管理
2. (fix) 完善了 Gradle 插件, 修复了当启用 kapt 插件时, annotationProcessor 不起作用的问题

### 0.10.18

1. (fix) 修复 update() 方法中错误的 SQL 构建

### 0.10.17

1. (fix) 修复 `joinByAnd` 和 `joinByOr` 中迭代器的错误, 他会导致 NoSuchElementException

### 0.10.16

1. (fix) 修复 page 方法中产生的 sql 语句错误(limit 在 count 子句中)
2. 分页页码从 1 开始

### 0.10.15

1. (fix) 修复了 `LocalDateTime` 字面量的微秒精度问题
2. 添加了 `cast` 函数, 并在 kotlin 中给 Expression 添加了 toXXX 等辅助转换方法

### 0.10.14

1. 添加了 `concat` / `concat_ws` 函数

### 0.10.13

1. 完善字面量表达式 lit ,支持更多的数据类型
2. 字面量表达式 lit 和预处理参数表达式 arg, 不能接受另外一个表达式作为值

### 0.10.12

1. 完善的 where 方法的逻辑, 如果 where 传入 null, 相当于没有调用
2. 添加了两个辅助方法, `joinByAnd` 和 `joinByOr`, 通过 `and / or` 将表达式集合组合起来.

### 0.10.11 \*

1. 弃用实体的 `from` 方法, 使用 `forInsert` 代替
2. (fix) 修复了 save 方法的 BUG, 该 BUG 可能会导致联合主键中有自增列, 而无法返回插入实体的问题

### 0.10.10 \*

1. 添加了 boolean 类型的支持, 当表字段被声明为 boolean 类型(实际上是 tinyint(1)), 而字段名以 is 开头, 则生成的实体中, 对应的字段会被设置为 Boolean 类型, 而不是 Integer 类型
2. (fix) 修复 IDEA 插件的 BUG, BUG: 当编写 sqlm 文件时, 刚刚输入方法名还没有来得及写其他内容的时候, IDEA 报 FoldingExpcetion
3. (fix) 给单实体生成的 SQL 中的 表名 / 字段名 添加反引号, 防止标识符带来的语法异常

### 0.10.9

1. 给表达式(Expression)添加了 `isNull` 的支持, 注意 `xxx is null` 和 `xxx = null` 是有差异的

### 0.10.8 \*

1. 给表达式添加了 `原生 SQL` 的支持
2. 给表达式添加 `in` 的支持
3. 完善了 `nullable` 信息的生成, 现在生成的实体类会加 kotlin 兼容的可空信息注解
