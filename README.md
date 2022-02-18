# JS-interview-questions

1. Write polyfill for getElementsByClassName
```
    function getElementsByClassName(className) {
      const body = document.body;
      const result = [];
      function traverse(element) {
        if (element.classList.contains(className)) {
          result.push(element);
        }
        for (let i = 0; i < element.children.length; i++) {
          traverse(element.children[i]);
        }
      }
      traverse(body);
      return result;
    }
```
2. Write polyfill of array.flat
```
function flat(arr, depth = 1, output = []) {
  if (depth === -1) {
    output.push(arr);
    return output;
  }

  for (const item of arr) {
    if (Array.isArray(item)) {
      flat(item, depth-1, output);
    } else {
      output.push(item);
    }
  }
  return output;
}
```
3. Write a polyfill of Promise
```
function MyPromise(executor) {
  let onResolve;
  let onReject;
  let isFullfilled = false;
  let isRejected = false;
  let isCalled = false;
  let value;
  let error;

  function resolve(val) {
    isFullfilled = true;
    value = val;
    if (typeof onResolve === 'function' && !isCalled) {
      onResolve(val);
      isCalled = true;
    }
  }
  function reject(err) {
    isRejected = true;
    error = err;
    if (typeof onReject === 'function' && !isCalled) {
      onReject(err);
      isCalled = true;
    }
  }
  this.then = function (thenHandler) {
    onResolve = thenHandler;
    if (!isCalled && isFullfilled) {
      onResolve(value);
      isCalled = true;
    }
    return this;
  }
  this.catch = function (catchHandler) {
    onReject = catchHandler;
    if (!isCalled && isRejected) {
      onReject(error);
      isCalled = true;
    }
    return this;
  }
  executor(resolve, reject);
}
```
4. Write a polyfill for fn.bind
```
Function.prototype.bind = Function.prototype.bind || function (obj, ...args) {
  return (...newArgs) => this.apply(obj, [...args, ...newArgs]);
};
```
