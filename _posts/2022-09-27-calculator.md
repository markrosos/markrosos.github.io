---
layout: post
title: Calculator/Everything I'm doing seems wrong
date: 2022-09-27 06:43:19 -0400
---

**It works, but it all feels wrong**

After taking a long break from this calculator project due to illness, I've come back to it, and almost instantly thought of a way to remove a lot of redundancy, while also trimming about a third of the total lines of code off of it. That's good, right? I'm not sure. It doesn't feel good.

Originally, I was putting numbers into one array, then shifting them into a second array (since when inputting '42' they showed up as [4,2] instead of [42]), operating on the numbers in that array, storing the result in a third array (very smart, I know), and then operating on that third array if I needed to switch operators, like from addition to subtraction. Seems dumb looking back.

```javascript
document.querySelectorAll('.nbox').forEach((btn) => {
  btn.addEventListener('click', (event) => {
    data.push(parseFloat(event.target.textContent));
    digits = Number(data.join(''));
    data = [digits];
  });
});
```

I'm still using this, but there's a problem with it that I'll get to later. Here's the old code:

```javascript
const combineNum = function () {
  data2.push(...data);
  data.length = 0;
};

const add = function (data2) {
  data3.length = 0;
  data3.push(data2.reduce((a, b) => a + b));
  return data2.reduce(
    (previousValue, currentValue) => previousValue + currentValue
  );
};

const pushAdd = function () {
  if (data2.length >= 2) {
    selections();
    selectAdd = true;
    data2.length = 0;
    data2.push(data3.reduce((a, b) => a - b));
  }
};

 const addBtn = document.querySelector('.add');
addBtn.addEventListener('click', () => {
  combineNum();
  operate();
  pushAdd();
  selections();
  selectAdd = true;
});
```

It worked, but in retrospect, it seems quite dumb to shift numbers around so much and perform operations in pushAdd() again. Now I'm just using this:

```javascript
const addTest = function (data2) {
  result = data2.reduce((a, b) => a + b);
  return result;
};

const arrayTest = function () {
  data2.length = 0;
  data2 = [result];
};

const operateTest = function () {
  combineNum();
  if (data2.length >= 2) {
    if (selectAdd == true) {
      addTest(data2);
    } else if (selectSubtract == true) {
      subtractTest(data2);
    } else if (selectDivide == true) {
      divideTest(data2);
    } else if (selectMultiply == true) {
      multiplyTest(data2);
    }
    arrayTest();
  }
};
```

When I call the operator function, it just calls addTest (or whichever operator), returns the result, then runs arrayTest(), which stores the result in a variable, clears data2[] of the numbers used in the previous operation, and pushes the result variable back into data2[] for further operations. No issues switching operators this way. The operator buttons determine which operator function to call. I guess that's simple? I don't know. Is it "best practices" to use if/else so many times? I don't know that either. It all seems to work, but with no feedback, I have the feeling that my code could be a horrow show to any experienced programmer.

Back to this event listener:

```javascript
document.querySelectorAll('.nbox').forEach((btn) => {
  btn.addEventListener('click', (event) => {
    data.push(parseFloat(event.target.textContent));
    digits = Number(data.join(''));
    data = [digits];
  });
});
```

I'm converting the text from the button to a number, pushing it into the data[] array, which unfortunately gives me individual numbers (again, [4,2] instead of [42]), meaning I have to join the numbers from the array and put them in a variable ('digits)', and then replace the numbers in the array with 'digits'. Does it work? Only until I try to use a decimal. I've searched for a very long time for a method to treat the decimal as a number before it's put into the array, but it always comes up with NaN in the array, meaning the entire thing falls apart.

I've come up with a solution, but I have no idea how to implement it. If I treat the numbers sent into data as a whole string ('1.42'), I can then just convert '1.42' into a number. How do I do that? I have no idea. Typing this has just made me realize that parseFloat in the above code is redundant though. Maybe this blog will be useful after all. Now how do I get ['1.42'] into that array instead of ['1','.','4','2']?




