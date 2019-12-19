---
title: 如何正确的使用Promise
date: 2019-12-19 16:15:56
tags: [promise,es5]
---
# promise用法
对比传统回调函数与Pormise的写法

传统回调函数

```javascript
// 声明函数
function run(callback) {
    let parmas = 0;
    if (callback) callback(parmas);
};
function fnStep1(callback) {
    let parmas = 123;
    if (callback) callback(parmas);
};
function fnStep2(callback) {
    let parmas = 456;
    if (callback) callback(parmas);
};
function fnStep3(callback) {
    let parmas = 789;
    if (callback) callback(parmas);
};
// fnStep4 ... 

// 传统使用回调的写法
run(function (parmas) {
    // parmas = 0
    console.log(parmas);
    fnStep1(function (parmas1) {
        // parmas = 123
        console.log(parmas1);
        fnStep2(function (parmas2) {
            // parmas = 456
            console.log(parmas2);
            fnStep3(function (parmas3) {
                // ...
                // 一直嵌套
            });
        });
    });
});


```

Promise的写法

```javascript

let p = new Promise((resolve, reject) => {
    // ?异步操作，最终调用:
    //
    const parmas = 0;
    resolve(parmas); // fulfilled
    // ?或
    //   reject("failure reason"); // rejected
})

p
    .then(
    (parmas) => {
        // parmas，resolve返回的值
        console.log(parmas);
        // 你的代码块 code...
        return 123; //返回值给下一个then
    }
    )
    .then(
    (parmas) => {
        // parmas，上一个then返回的值
        console.log(parmas);
        // 你的代码块 code...
        return 456; //返回值给下一个then
    }
    )
    .then(
    (parmas) => {
        // parmas，上一个then返回的值
        console.log(parmas);
        // 你的代码块 code...
        return 789; //返回值给下一个then
    }
    )

```

Promise要比传统回调函数更简洁直观，可读性更强。

那如何使用Promise进行异步回调? 如何捕获错误？

```javascript
// 声明函数
function asyncFn(a) {

    return new Promise((resolve, reject) => {
        a += 1;
        setTimeout(function () {
            // 使用resolve则返回a
            resolve(a);
            // 使用reject则返回错误，并结束then的继续向下执行，并会跳到catch
            // reject(new Error("fail"));
        }, 2000);
    });

}

// 执行
asyncFn(1).then(
    (a) => {
        // 过了2秒后接收到a值 => 2
        console.log(a);

        const newVal = 5;
        // const newVal = {a: 5};
        // const newVal = new Promise((resolve, reject) =>{});
        // 返回值可以是数字，字串，对象或者是 Promise
        return newVal;
    }
).then(
    (newVal) => {
        // newVal 获得上一个then返回的值 或 返回的Promise的返回值

    }
).catch(
    (err)=>{
        // 如用到reject，则会直接跳到此处
        console.log(err)
    }
);

```