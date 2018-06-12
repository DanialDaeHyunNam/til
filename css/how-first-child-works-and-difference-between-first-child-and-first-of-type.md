## How :first-child works and difference between first-child and first-of-type

#### html
```html
<body>
    <div class="editor">
        <div class="name">Name</label>
    </div>
    ...
</body>
```
#### css
```css
body > div:first-child{
  margin: 0;
}

.editor:fisrt-child{
  color: red;  
}
```

위와 같이 실행하면 **first-child** 는 어떤경우에도 적용되지 않는다. 그 이유는 first-child를 하게되면, 위의 경우에는 div의, 혹은 .editor의 부모 엘리먼트를 확인해서 우리가 지정한 엘리먼트가 첫 번째 자식 엘리먼트에 해당할 때 적용하라는 의미이기 때문이다.
<br>
그래서 이런경우엔 **first-of-type** 을 쓰게되면 적용될 수 있으나, E9+ 와 다른 브라우저에서만 적용되기 때문에 조심해야 한다.

## Reference
https://stackoverflow.com/questions/7589841/why-doesnt-this-css-first-child-selector-work
