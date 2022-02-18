# JS-interview-questions

1. Write polyfill for getElementsByClassName
`
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
`
2. Write polyfill of array.flat
`
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
`
3. Write a polyfill of Promise
`
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
`
4. Write a polyfill for fn.bind
`
Function.prototype.bind = Function.prototype.bind || function (obj, ...args) {
  return (...newArgs) => this.apply(obj, [...args, ...newArgs]);
};
`
5.Rendering of a page:
```
1. The rendering engine starts getting the contents of the requested
  document from the networking layer. This will usually be done in 8kB chunks.
2. A DOM tree is built out of the broken response.
3. New requests are made to the server for each new resource that is
  found in the HTML source (typically images, style sheets, and JavaScript files).
4. At this stage the browser marks the document as interactive and
  starts parsing scripts that are in "deferred" mode: those that 
  should be executed after the document is parsed. The document
  state is set to "complete" and a "load" event is fired.
5. Each CSS file is parsed into a StyleSheet object, where each
  object contains CSS rules with selectors and objects corresponding
  CSS grammar. The tree built is called CSSCOM.
6. On top of DOM and CSSOM, a rendering tree is created, which is a set of
  objects to be rendered. Each of the rendering objects contains its
  corresponding DOM object (or a text block) plus the calculated styles.
  In other words, the render tree describes the visual representation of a DOM.
7. After the construction of the render tree it goes through a "layout" process.
  This means giving each node the exact coordinates where it should appear on the screen.
8. The next stage is painting–the render tree will be traversed and each
  node will be painted using the UI backend layer.
9. Repaint: When changing element styles which don't affect the element's
  position on a page (such as background-color, border-color, visibility),
  the browser just repaints the element again with the new styles applied (that means a "repaint" or "restyle" is happening).
10. Reflow: When the changes affect document contents or structure, or element position, a reflow (or relayout) happens.
```
6.
`
fixed and sticky

fixed position will not occupy any space in the body, so the next element(eg: an image) will be behind the fixed element.

sticky position occupies the space, so the next element will not be hidden behind it.

position: relative
it is similar to static but top, left, right, bottom are applied to the element with respect to its original position.
`
7.
`
lifecycle methods
Mounting phase:
  constructor: first method that is called
  static getDerivedStateFromProps is a new React lifecycle method as of React 17 designed to replace componentWillReceiveProps.
  render method
  componentDidMount: grab dom node, set event listeners, call api calls, etc.

Updating phase:
  static getDerivedStateFromProps()
  shouldComponentUpdate(), alternative: React.PureComponent
  getSnapshotBeforeUpdate(prevProps, prevState) and componentDidUpdate(prevProps, prevState, snapshot)

Unmounting phase:
  componentWillUnmount()

Error handling:
  static getDerivedStateFromError(error)
  componentDidCatch(error, info)
`
8.
`
Responsive techniques:

Leverage conditional loading.
Make the layouts fluid/adaptive by default.
Choose the right breakpoint for the layout.
Use media queries to control the layout.
Use flexbox and grid to control the layout.
Consider the landscape orientation.
Keep the typography responsive.
Leverage mobile devices' Native Hardware.
Design for thumb.
`
9.
`
em: font-size is relative to the font-size of the current element
rem: font-size is relative to the font-size of the root element
`
10.
`
Q. what is prototype
Ans: prototype is a javascript object that is used to create objects. 
prototype is a prototype object that is used to create objects.
`
11.`
box-sizing
content-box: width and height do not include padding and border
border-box: width and height include the border, padding
`
12.
`animate using RAF`
13.
`
display: inline-block;
Compared to display: inline, the major difference is that display: inline-block allows to set a width and height on the element.

Also, with display: inline-block, the top and bottom margins/paddings are respected, but with display: inline they are not.

Compared to display: block, the major difference is that display: inline-block does not add a line-break after the element, so the element can sit next to other elements.
`
