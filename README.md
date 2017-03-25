# nicemark: markdown structures

> nicemark is a simple extension to the fantastic and fast marked JavaScript compiler.

### **[Try it now!](http://goldenforever.github.io/nicemark)**

It inherits marked's features plus makes the following additions and changes:

## Additions

### Columns

**Input**

```
] ## Col 1
]
] - List 1
] - List 2
    ] ## Col 3
    ]
    ] Paragraph to
    ] demonstrate.
  ] ## Col 2
  ] 
  ] The *indent*
  ] determines the
  ] column order.
```

**Output**
```html
<div class="columns" style="display:flex">
  <div class="column" style="order:0">
    <h2 id="col-1">Col 1</h2>
    <ul>
      <li>List 1</li>
      <li>List 2</li>
    </ul>
  </div>
  <div class="column" style="order:4">
    <h2 id="col-3">Col 3</h2>
    <p>Paragraph to
    demonstrate.</p>
  </div>
  <div class="column" style="order:2">
    <h2 id="col-2">Col 2</h2>
    <p>The <strong>indent</strong>
    determines the
    column order.</p>
  </div>
</div>
```

### Underline
**Input**
```
_This used to be italic but makes more sense as an underline._
```

**Output**
```html
<span class="underline"><u>This used to be italic but makes more sense as an underline.</u></span>
```

> Depending on your use case either the span or the u tag will be better, but having both will get both an appropriate default appearance and the option of a non-deprecated alternative with this in your stylesheet:
> 
> ```css
> .underline {
>   text-decoration: underline;
> }
> ```

## Changes

> These changes can be disabled by choosing setting the pedantic option to `true`. This will disable underlines from underscores.

### Bold and Italic are reversed
Despite bold being much more common, italic would need only one star on either side whereas bold would need two; **that has been swapped around**.

Before: `*text*` --> `<em>text</em>`, and `**text**` --> `<strong>text</strong>`.  
After: `*text*` --> `<strong>text</strong>`, and `**text**` --> `<em>text</em>`.

### Bold and Italic Don't Accept Underscores
The `<strong>` and `<em>` tags will not be rendered by underscores on either side, as the underline uses it.

## Usage

Minimal usage:

```js
var nicemark = require('nicemark');
console.log(nicemark('I am using __markdown__.'));
// Outputs: <p>I am using <strong>nicemark</strong>.</p>
```

Example setting options with default values:

```js
var nicemark = require('nicemark');
nicemark.setOptions({
  renderer: new nicemark.Renderer(),
  gfm: true,
  tables: true,
  breaks: false,
  pedantic: false,
  sanitize: false,
  smartLists: true,
  smartypants: false
});

console.log(nicemark('I am using __markdown__.'));
```

### Browser

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8"/>
  <title>NiceMark in the browser</title>
  <script src="nicemark.min.js"></script>
</head>
<body>
  <div id="content"></div>
  <script>
    document.getElementById('content').innerHTML =
      nicemark('# Nicemark in browser\n\nRendered by **nicemark**.');
  </script>
</body>
</html>
```

For any further documentation, check out chjj/[marked](https://github.com/chjj/marked) for (some excellent) usage instructions.
