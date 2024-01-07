# Polyfills

A polyfill is a piece of code that provides functionality that is not natively supported by a web browser. The term "polyfill" is a combination of "poly," meaning many, and "fill," indicating that it fills in the gaps or provides support for features that may be lacking in certain environments.

For example, if a web browser does not support a particular JavaScript method or API, developers can use a polyfill to add that functionality, making it available in the unsupported browser.

```jsx
<!-- Polyfill for Array.prototype.map -->

<script>
    if (!Array.prototype.map) {
       Array.prototype.customMap = function(callback) {
            let newArray = []
						for(let i = 0 ; i < this.length ; i++){
              newArray.push(callback(this[i]))
            }
            	return newArray
        }
    }
</script>

<!-- Main application script -->
<script>
    var numbers = [1, 2, 3, 4, 5];

    var squaredNumbers = numbers.customMap(function (num) {
        return num * num;
    });

    console.log(squaredNumbers); // Output: [1, 4, 9, 16, 25]
</script>
```

## Implement a polyfill that mimics the implementation of the **`getElementById`** method?

```jsx
str = `
<body>

    <h1 id="a" >This is an H1 Heading</h1>
    
    <h1>This is an H2 Heading</h1>
    
    <h1 id="a">This is an H3 Heading</h1>

</body>
`;

dom = new DOMParser().parseFromString(str , 'text/html')
console.log(dom.body)

function dfs(element , id , result){
  if(result.length == 1) return
  if(element == null) return
    if(element.id == id) {
      result.push(element)
      return
  	}

  for(const child of element.children){
    dfs(child , id , result)
  }
}

function getelementbyid (body , id){
  const result = []
  for (const bodychild of body.children){
    dfs(bodychild , id , result)
  }
console.log(result)
}
getelementbyid(dom.body , "a")
```

## Implement a polyfill that mimics the implementation of the **getElementsByClassName** method?

```jsx
str = `
<body>

    <h1 class="a" >This is an H1 Heading</h1>
    
    <h1>This is an H2 Heading</h1>
    
    <h1 class="a">This is an H3 Heading</h1>

</body>
`;

dom = new DOMParser().parseFromString(str , 'text/html')

function dfs(element , classname , result){
  if(element == null) return
  for(const list of element.classList){
    if(list == classname) {
      result.push(element)
      return
    }
  }
  for(const child of element.children){
    dfs(child , classname , result)
  }
}

function getelementbyclass (body , classname){
  const result = []
  for (const bodychild of body.children){
    dfs(bodychild , classname , result)
  }
console.log(result)
}
getelementbyclass(dom.body , "a")
```

## Implement a polyfill that mimics the implementation of the **getElementsByTagName** method?

```jsx
str = `
<body>

    <h1 class="a" >This is an H1 Heading</h1>
    
    <h1>This is an H2 Heading</h1>
    
    <h1 class="a">This is an H3 Heading</h1>

</body>
`;
dom = new DOMParser().parseFromString(str , 'text/html')
console.log(dom.body)

function dfs(element , tagname , result){
  	if(element == null) return
    if(element.tagName == tagname) {
      result.push(element)
      return
    }
  for(const child of element.children){
    dfs(child , tagname , result)
  }
}

function getelementbytagname (body , tagname){
  const result = []
  for (const bodychild of body.children){
    dfs(bodychild , tagname , result)
  }
console.log(result)
}
getelementbytagname(dom.body , "H1")  // element.tagName returns capitalised tagname
```
