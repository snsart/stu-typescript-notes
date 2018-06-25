### 作用域
var 声明的变量的作用域属于整个函数，它没有块级作用域，变量在函数内部的任何位置都能被访问到；<br>
let 声明的变量，使用的是块级作用域，块作用域变量在包含它们的块或for循环之外是不能访问的，拥有块级作用域的变量的另一个特点是，它们不能在被声明之前读或写。

### 重定义及屏蔽
var 声明变量时它不在乎你声明多少次；你只会得到1个。
```typeScript
function f(x) {
    var x;
    var x;

    if (true) {
        var x;
    }
}
```
let 在同一个作用域中对变量只能声明一次，以下声明方式都会报错：
```typeScript
let x = 10;
let x = 20; // 错误，不能在1个作用域里多次声明`x`

function f(x) {
    let x = 100; // error: interferes with parameter declaration
}

function g() {
    let x = 100;
    var x = 100; // error: can't have both declarations of 'x'
}
```
在嵌套作用域内部重新声明一个变量的行为称为屏蔽，内部变量会屏蔽掉外部变量，为了代码的清晰，通常不要使用，应分开定义两个名字不同的变量。
```typeScript
for (let i = 0; i < matrix.length; i++) {
    var currentRow = matrix[i];
    for (let i = 0; i < currentRow.length; i++) {
        sum += currentRow[i];
    }
}
```

### 块级作用域变量的获取
对于var或let声明的变量，每次进入一个作用域时，它创建了一个变量的环境。 就算作用域内代码已经执行完毕，这个环境与其捕获的变量依然存在。
当let声明出现在循环体里时拥有完全不同的行为。 不仅是在循环里引入了一个新的变量环境，而是针对每次迭代都会创建这样一个新作用域。 这就是我们在使用立即执行的函数表达式时做的事，所以在 setTimeout例子里我们仅使用let声明就可以了。
```typeScript
for (let i = 0; i < 10 ; i++) {
    setTimeout(function() {console.log(i); }, 100 * i);
}
```
以上代码会输出：0 1 2 3 4 5 6 7 8 9，当把let换成var时，输出9 9 9 9 9 9 9 9 9

### const声明
它们与let声明相似，但是就像它的名字所表达的，它们被赋值后不能再改变。 换句话说，它们拥有与 let相同的作用域规则，但是不能对它们重新赋值。

