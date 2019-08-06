
## rpn-calculator

### RPN 简介

RPN(reverse polish notation)，反向波兰表示法，也称为波兰后缀表示法或简称后缀表示法，是一种数学符号，其中运算符遵循其操作数，与波兰符号（PN）相反，其中运算符在其操作数之前。只要每个运算符具有固定数量的操作数，它就不需要任何括号。 “波兰”是指逻辑学家 Jan Łukasiewicz 的国籍，他于1924年发明了波兰符号。

如下可以看一些例子：

| 代数表达                         | RPN               | 
| -- | -- |
| 3 + 5                           | 3 5 +             |
| 6 * ( 7 + 8 )                   | 6 7 8 + *         |
| ( 9 + 5 ) * ( 7 + 8 )           | 5 + 7 8 + *       |
| ( ( 4 * ( 2 – 3 ) ) / ( 5 – 6 ) | 4 2 3 – * 5 6 – / |


在反向波兰表示法中，运算符在其操作数之后; 例如，要3和4进行加法，一个将写入`3 4 +`而不是`3 + 4`。如果有多个操作，则在第二个操作数之后立即给出运算符; 因此，用常规符号写成`3 - 4 + 5`的表达式将以反向波兰符号写成`3 4 - 5 +`:首先从3中减去4，然后加5。 反向波兰表示法的一个优点是它不需要中缀表示法所需的括号。 虽然`3 - 4 × 5` 也可以写成`3 - (4 × 5)`，与`(3 - 4) × 5`完全不同。在反向波兰表示法中，前者可以写成`3 4 5 × -` ，这是毫不含糊的意味着`3 (4 5 ×) -` 到 `3 20  -`; 后者可以写成`3 4  -  5 ×`（如果保持相似的格式，也可以是`5 3 4  - ×`），这明确地是指`(3 4  - ) 5 ×`。

### RPN 计算器

该计算器等待用户输入并期望接收包含空格的字符串来分开的数字和运算符列表。
 
数字被推入堆栈。运算符对堆栈中的数字进行操作。

所有可用的运算符包括 `+`、`-`、`*`、`/`、`sqrt`、`undo`、`clear`。

运算符将其参数从堆栈中弹出，并将其结果推回到堆栈中。

- `clear` 操作将清空堆栈。
- `undo` 操作会撤销回退上一步操作，“undo undo” 会撤销先前的两步操作。
- `sqrt` 操作会为栈顶元素执行开平方操作。
- `+`、`-`、`*`、`/` 操作则对应的是加、减、乘、除，其操作数为栈顶部的两个元素。

处理完输入字符串后，计算器会将堆栈的当前内容显示为以空格分隔的列表。 数字存储在堆栈中至少精确到15位小数，但显示为10位小数（如果不会导致精度损失，则显示为小数）。
 
如果运算符在堆栈上找不到足够数量的参数，则会显示警告：
 
`operator <operator> (position: <pos>): insufficient parameters`

显示警告后，字符串的所有接下来的处理会终止，并显示堆栈的当前状态。
