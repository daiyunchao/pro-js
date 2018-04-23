# Array 类型

除了Object 之外，Array 类型恐怕是ECMAScript 中最常用的类型了。而且，ECMAScript 中的数组与其他多数语言中的数组有着相当大的区别。ECMAScript 数组的每一项可以保存任何类型的数据。

```javascript
var colors = ["red", "blue", "green"]; // 定义一个字符串数组
alert(colors[0]); // 显示第一项
colors[2] = "black"; // 修改第三项
colors[3] = "brown"; // 新增第四项
```

```javascript
var colors = new Array(3); // 创建一个包含3 项的数组
var names = new Array("Greg"); // 创建一个包含1 项，即字符串"Greg"的数组
```

由于数组最后一项的索引始终是length-1，因此下一个新项的位置就是length。每当在数组末尾添加一项后，其length 属性都会自动更新以反应这一变化。

数组最多可以包含4 294 967 295 个项，这几乎已经能够满足任何编程需求了。如果想添加的项数超过这个上限值，就会发生异常。而创建一个初始大小与这个上限值接近的数组，则可能会导致运行时间超长的脚本错误。

---

# ES6为  添加了不少的方法

1. find(function(currentItemValue,currentIndex,currentArray){}) 

查找数组第一个匹配项
参数说明:currentItemValue:当前该项的值, currentIndex:当前下标 currentArray:当前数组本身
``` javascript

let arr=[1,2,234,'sdf',-2];
arr.find(function(x){
    return x<=2;
})//结果：1，返回第一个符合条件的x值
arr.find(function(x,i,arr){
    if(x<2){console.log(x,i,arr)}
})//结果：1 0 [1, 2, 234, "sdf", -2]，-2 4 [1, 2, 234, "sdf", -2]

```

2. findIndex(function(currentItemValue,currentIndex,currentArray){})

查找数组第一个匹配项的下标
参数说明:currentItemValue:当前该项的值, currentIndex:当前下标 currentArray:当前数组本身
``` javascript

let arr=[1,2,234,'sdf',-2];
arr.findIndex(function(x){
    return x<=2;
})//结果：0，返回第一个符合条件的x值的索引
arr.findIndex(function(x,i,arr){
    if(x<2){console.log(x,i,arr)}
})//结果：1 0 [1, 2, 234, "sdf", -2]，-2 4 [1, 2, 234, "sdf", -2]

```

3. includes(findValue,findStart)
数组是否包含[findValue]值
参数说明:findValue:需要查找的值, findStart:查找开始的下标

``` javascript

let arr=[1,2,234,'sdf',-2];
arr.includes(2);// 结果true
arr.includes(20);// 结果：false
arr.includes(2,3)//结果：false

```

4. keys()

找出数组的全部下标,并且组成数组返回一个 **迭代器**

``` javascript

let arr=[1,2,234,'sdf',-2];
console.log(arr.keys());//Array Iterator {}
for(let a of arr.keys()){
    console.log(a)
}//结果：0,1,2,3,4  遍历了数组arr的索引


```

5. values()

找出数组的全部值,并且组成数组返回一个 **迭代器**

``` javascript

let arr=[1,2,234,'sdf',-2];
for(let a of arr.values()){
    console.log(a)
}//结果：1,2,234,sdf,-2 遍历了数组arr的值

```

6. entries()

将数组的每一项,构建成[下标,下标对应的值]

``` javascript

let arr=['w','b'];
for(let a of arr.entries()){
    console.log(a)
}//结果：[0,w],[1,b]
for(let [i,v] of arr.entries()){
    console.log(i,v)
}//结果：0 w,1 b

```

7. fill(withFillValue,startIndex,endIndex)

用固定值,填充数组
参数: withFillValue:填充的值 startIndex:填充开始位置, endIndex:填充的结束位置 **注意:该方法会改变原数组**

``` javascript

let arr=['w','b'];
arr.fill('i')//结果：['i','i']，改变原数组
arr.fill('o',1)//结果：['i','o']改变原数组,第二个参数表示填充起始位置
new Array(3).fill('k').fill('r',1,2)//结果：['k','r','k']，第三个数组表示填充的结束位置

```

8. Array.of()

Array.of方法用于将一组值，转换为数组。Array.of总是返回参数值组成的数组。如果没有参数，就返回一个空数组
Array.of基本上可以用来替代Array()或new Array()，并且不存在由于参数不同而导致的重载。它的行为非常统一

``` javascript

//使用Array的问题
Array() // []  
Array(3) // [, , ,] 
Array(3, 11, 8) // [3, 11, 8]  

//为了解决这个问题,引入了 Array.of

Array.of() // []  
Array.of(3) // [3]  
Array.of(3, 11, 8) // [3,11,8] 
Array.of(undefined) // [undefined] //总是返回一个数组,无论传递什么参数
//可以看到 无论给Array.of函数传递什么参数,返回的值都是统一的,不会因为参数的数量不同,导致出现结果不同的问题

```

9. copyWithin(target,start=0,endIndex=this.length)

将某些个位置的元素复制并覆盖到其他位置上去
参数说明: target: 从该位置开始替换数据 start:从该位置开始读取数据，默认为 0 。如果为负值，表示倒数 endIndex:到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数

``` javascript
 //将 3 号位复制到 0 号位
[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
//[4, 2, 3, 4, 5] 

// -2 相当于 3 号位， -1 相当于 4 号位  
[1, 2, 3, 4, 5].copyWithin(0, -2, -1)  
// [4, 2, 3, 4, 5]  

```

10. Array.from(object)

将其他类型数据转换成数组
参数: object:满足两个条件:
- 部署了Iterator接口的对象，比如：Set，Map，Array。
- 类数组对象，什么叫类数组对象，就是一个对象必须有length属性，没有length，转出来的就是空数组

``` javascript

//转换map
const map1 = new Map();
map1.set('k1', 1);
map1.set('k2', 2);
map1.set('k3', 3);
console.log('%s', Array.from(map1))
//k1,1,k2,2,k3,3

//转换set
const set1 = new Set();
set1.add(1).add(2).add(3)
console.log('%s', Array.from(set1))
//1,2,3

//转换字符串
console.log('%s', Array.from('hello world'))
console.log('%s', Array.from('\u767d\u8272\u7684\u6d77'))
//h,e,l,l,o, ,w,o,r,l,d
//白,色,的,海

//类数组:,可用于arguments
console.log('%s', Array.from({
  0: '0',
  1: '1',
  3: '3',
  length:4
}))
//0,1,,3

//如果不是类数组,则会返回空数组

console.log('%s', Array.from({
  a: '1',
  b: '2',
  length:2
}))
//[]
```

