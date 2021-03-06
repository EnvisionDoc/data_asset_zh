# 多路数据归并处理表达式语法

多路数据归并处理策略中输出逻辑表达式支持的常见语法如下表所示：

.. list-table::
   :widths: 20 20 60

   * - 表达式符号
     - 说明
     - 描述
   * - $
     - 变量选择符
     - 使用方法为：`​${ 变量 }`，`变量`必须是已创建的模型、模型测点或者属性。
   * - if...else
     - 条件判断语句
     - 当条件为 true 时执行代码，条件为 false 时执行其它代码。格式为：``if (条件) { 当条件为 true 时执行的代码 } else { 当条件不为 true 时执行的代码 }``
   * - if...else if...else
     - 条件判断语句
     - 用于选择多个代码块之一执行。格式为：``if (条件 1) { 当条件 1 为 true 时执行的代码 } else if (条件 2) { 当条件 2 为 true 时执行的代码 } else { 当条件 1 和 条件 2 都不为 true 时执行的代码 }``
   * - "::"
     - 名称空间标识符
     - 参考C++语法。格式为：``类名称（模型）``::``该类的成员名称（模型测点或者模型属性）``。
   * - "+ - * /"
     - 算数运算符
     - 加、减、乘、除等算数运算符
   * - "! && |"
     - 逻辑运算符
     - 逻辑非、逻辑与、逻辑或

.. note:: 多路归并数据处理表达式支持Scala语法，EnOS流数据分析禁止for和while等循环语句。

## 变量自动提示功能

在编写输出逻辑表达式时，输入变量提示符之后，支持自动提示组织内所有的模型、模型测点、模型属性。示例如下：

.. image:: ../media/autocomplete.gif

## 表达式范例解释

```scala
if(${turbine::wind_speed} > 50) {
    ${turbine::power}+10
}
else {
    ${turbine::power}-10
}
```

上述表达式的含义是：如果 `wind_speed` 大于50，则输出 `power+10`，否则输出 `power-10`。



<!--end-->
