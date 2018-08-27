# language-tips
一些有用的代码
### 1.得到页面滚动的距离  
```javascript
  const scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
```
### 2.防抖
所谓防抖，就是指触发事件后在n秒内函数只能执行一次，如果在n秒内又触发了时间，则会重新计算函数执行时间。
```javascript
  /**
   * @desc 函数防抖
   * @param func函数
   * @param wait延迟执行毫秒数
   * @param immediate true 表示立即执行， false表示非立即执行
   ** /   
```
```javascript
  function debounce(func, wait, immediate) {
    let timeout;

    return function () {
      let context = this;
      let args = arguments;

      if(timeout) clearTimeout(timeout);
      if(immediate) {
        let callNow = !timeout;
        timeout = setTimeout(function () {
          timeout = null;
        }, wait)
        if(callNow) func.apply(context, args)
      } else {
        timeout = setTimeout(function() {
          func.apply(context, args)
        }, wait)
      }
    }
  }
```
### 3.节流
节流，就是指连续触发事件但是在n秒中只执行一次函数。
```javascript
  /**
   * @desc 函数节流
   * @param func函数
   * @param wait延迟执行毫秒数
   * @param type 1表示时间戳版， 2 表示定时器版
   * /
```
```javascript
  function throttle (func, wait, type) {
    if(type === 1) {
      var previous = 0
    } else if(type === 2) {
      var timeout;
    }

    return function () {
      let context = this;
      let args = arguments;
      if(type === 1) {
        var now = Date.now();
        if(now - previous > wait) {
          func.apply(context, args);
          previous = now;
        }
      } else if (type === 2) {
        if(!timeout) {
          timeout = setTimeout(function() {
            timeout = null;
            func.apply(context, args);
          }, wait)
        }
      }
    }
  }
```

