---
layout: post
title: Calculator Finished?
date: 2022-09-30 07:53:06 -0400
---

** Progress, finally? **

First, the project link:
--project url: [https://markrosos.github.io/Calculator/](https://markrosos.github.io/Calculator/)
--repository: [https://github.com/markrosos/Calculator](https://github.com/markrosos/Calculator)

Finally made it back to my calculator project and figured out a very simple way to add the numbers as a string to the first array, and then convert them to a number in the second array. Onto my decimal issue:

```javascript
document.querySelectorAll('.nbox').forEach((btn) => {
  btn.addEventListener('click', (event) => {
    data.push(event.target.textContent);
    digits = data.join('');
    data = [digits];
  });
});
```

Previously I was converting the string to a number when using the join() function, so all it took was removing Number(data.join('')) to input a number with a decimal (as a string) into the array. Seems unbelievably simple looking back. I think I was trying to find complicated solutions to easy problems. It took me a bit to figure out how to then convert the string into a number when pushing it to data2[], but of course the solution to that was simple too:

```javascript
const combineNum = function () {
  data2.push(Number(...data));
  data.length = 0;
};
```

I fiddled around with trying to convert it with the button press event, but I couldn't get that to work. Again, seems obvious looking back, but I still feel like there should be a way to convert 'digits' to a number before it's defined as the data[] array again. 

I (kind of) solved my dumb if else problem by putting it into its own function as follows:

```javascript
const selectionRules = function () {
  if (selectAdd) add(data2);
  else if (selectSubtract) subtract(data2);
  else if (selectDivide) divide(data2);
  else if (selectMultiply) multiply(data2);
};
```

Yeah, it's doing the same thing as before, but there are less lines, it's easier to read, and there is no longer an if nested under an if. That previous if is still in the operate function, but there's only one:

```javascript
const operate = function () {
  combineNum();
  if (data2.length >= 2) {
    selectionRules();
    shiftNum();
    selections();
  }
};
```

I'm still unsure if calling all of these functions inside of a function is 'bad practice' or not. This is another point where I could really use some feedback, but I truly am on my own here. It all works though.

There were two more problems to solve, which was the Clear button, and Delete button. Both were easy. Maybe I'm getting better at this? Or maybe I'm just getting better at google. I at least knew what to look for when it came to removing items, which was the slice() function. Here's what I came up with:

```javascript
clearButton.addEventListener('click', () => {
  innerdisplay.textContent = '';
  data.length = 0;
  data2.length = 0;
});

deleteButton.addEventListener('click', () => {
  data = data.map((data) => data.slice(0, -1));
  innerdisplay.textContent = innerdisplay.textContent.slice(0, -1);
});
```

This was really simple. I'm almost proud of how quickly I solved this problem. I'm sure an experienced developer could do this in a minute, but it wasn't the hours-long problem I was worried it would be. Is the whole project done? I think it's done. I might make some minor aesthetic changes, but everything works, and everything looks okay. I should probably move on anyway, I doubt I'm learning all that much continuing to fiddle with this. I did learn a lot though. Let's hope that becomes a trend.