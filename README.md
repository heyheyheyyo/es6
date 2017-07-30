
//////////////////// 数组的解构赋值 /////////////////
// 1. 赋值
let x11 = 1;
let y11 = 2;
let z11 = 3;
// 现在可以写成
let [x12, y12 ,z12] = [1,2,3];

// 2.其他写法
let [x21, [[y21], z21]] = [1, [[2], 3]];
let [ , , x22] = ['foo', 'bar', 'baz'];
let [x23, , y23] = [1, 2, 3];
let [head2, ...tail2] = [1, 2, 3, 4];
let [x24, y24, ...z24] = ['a'];

// 3. 解构失败
let [x31] = [];
let [x32, y32] = [1];

// 4. 不完全解构
let [x41, y41] = [1, 2, 3];
let [x42, [y42], y43] = [1, [2, 3], 4];

// 5. 右边不是数组
let [x51] = 1;
let [x52] = false;
let [x53] = NaN;
let [x54] = undefined;
let [x55] = null;
let [x56] = {};

// 5. 其他带有Iterator接口的结构
let [x5, y5, z5] = new Set(['a', 'b', 'c']);

// 6. 默认值 解构赋值允许设置默认值
let [x61 = true] = [];
let [x62, y62 = 'b'] = ['a']; 
let [x63, y63 = 'b'] = ['a', undefined]; 

// 7. 默认值需要严格相等于()
let [x7 = 1] = [null];

// 8. 如果默认值是个函数
function f() {
  return 3;
}
let [x8 = f()] = [1]; 

// 9. 默认值可以用变量，但要声明过
let [x91 = 1, y91 = x91] = [];   
let [x92 = 1, y92 = x92] = [2];    
let [x93 = 1, y93 = x93] = [1, 2]; 
let [x94 = y94, y94 = 1] = [];     



//////////////////// 对象的解构赋值 /////////////////
// 1. 对象也可以解构赋值
let { a1, b1 } = { a1: 'aaa', b1: 'bbb' };

// 2.数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
let { a2, b2 } = { b2: 'bbb' , a2: 'aaa' };
let { c2 } = { a2:'aaa' , b2: 'bbb'}

// 3.如果变量名与属性名不一致，必须写成下面这样。
let { b3:c3 } = { a3:'aaa', b3:'bbb' }

// 4. 所以说对象的解构赋值满足下面的匹配模式
let { a4: a4, b4: b4 } = { a4: 'aaa', b4: 'bbb' };

// 5.与数组一样，解构也可以用于嵌套结构的对象。
let obj5 = {
  p: [
    'Hello',
    { b5: 'World' }
  ]
};
let { p: [a5, { b5 }] } = obj5;

// 6. 求 obj6 和 arr6
let obj6 = {}
let arr6 = []
({ foo: obj6.prop, bar: arr[0] } = { foo: 123, bar: true });

// 7. 默认值也是严格相等于 undefined
let {a7 = 3} = {};

// 8. 对象的解构赋值，可以很方便地将现有对象的方法，赋值到某个变量。
let { log, sin, cos } = Math;


//////////////////// 函数的解构赋值 /////////////////
// 1. 函数也可以解构赋值
function add([x, y]){
  return x + y;
}
add([1, 2]); 
//函数add的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量x和y。对于函数内部的代码来说，它们能感受到的参数就是x和y。

// 2. 另一个例子
[[1, 2], [3, 4]].map(([a, b]) => a + b);

// 3. 也可以设置默认值，当undefined的时候
function move({x = 0, y = 0} = {}) {
  return [x, y];
}
move({x: 3, y: 8}); 
move({x: 3}); 
move({}); 
move(); 


//////////////////// 字符串、数值、布尔值的解构赋值 /////////////////
// 1. 字符串也可以解构赋值
const [o, p, q, r, s] = 'hello';

// 2. 类似数组的对象都有一个length属性，
let {length : len} = 'hello';

// 3. 如果等号右边是数值和布尔值，则会先转为对象
let {toString: t31} = 123;
t31 === Number.prototype.toString // true
let {toString: t32} = true;
t32 === Boolean.prototype.toString // true


//////////////////// 用途 /////////////////
// 1. 交换变量的值
let x = 1;
let y = 2;
[x, y] = [y, x];

// 2. 从函数返回多个值 -- 返回一个数组
function example() {
  return [1, 2, 3];
}
let [a, b, c] = example();

// 3. 返回一个对象 -- 返回一个对象
function example() {
  return {
    foo: 1,
    bar: 2
  };
}
let { foo, bar } = example();

// 4. 函数参数的定义 -- 参数是一组有次序的值
function f([x, y, z]) { return; }
f([1, 2, 3]);

// 5. 函数参数的定义 -- 参数是一组无次序的值
function f({x, y, z}) { return; }
f({z: 3, y: 2, x: 1});

// 6. 提取JSON数据
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};
let { id, status, data: number } = jsonData;

// 7. 函数参数的默认值
let fun = function(x = 3){
    return 4 * x;
    // return x? 4 * x : 12
}
fun()

// 8. 输入模块的指定方法
import { aa, bb } from cc;

// 9. 遍历Map结构
//以后再说
