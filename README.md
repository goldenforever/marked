# nicemark: markdown structures

> nicemark is a simple extension to the fantastic and fast marked JavaScript compiler.

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
```
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
```
<span class="underline"><u>This used to be italic but makes more sense as an underline.</u></span>
```

> Depending on your use case either the span or the u tag will be better, but having both will get both an appropriate default appearance and the option of a non-deprecated alternative with this in your stylesheet:
> 
> ```
> .underline {
>   text-decoration: underline;
> }
> ```

## Changes

> These changes can be disabled by choosing setting the pedantic option from marked to `true`.

### Bold and Italic are reversed
Despite bold being much more common, italic would need only one star on either side whereas bold would need two; **that has been swapped around**.

Before: `*text*` => `<em>text</em>`, and `**text**` => `<strong>text</strong>`.  
After: `*text*` => `<strong>text</strong>`, and `**text**` => `<em>text</em>`.

### Bold and Italic Don't Accept Underscores
The `<strong>` and `<em>` tags will not be rendered by underscores on either side, as the underline uses it.

## Usage
See [marked's page](https://github.com/chjj/marked) for its excellent usage instructions.

I have for now kept the relevant functions named as 'marked' as it has not really been changed so much as to justify a full name change yet.
