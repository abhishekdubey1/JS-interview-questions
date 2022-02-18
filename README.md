# JS-interview-questions

Write polyfill for getElementsByClassName
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
