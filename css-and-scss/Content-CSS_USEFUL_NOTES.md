# CSS Useful Notes

## CSS Selectors and Rules
In order to tell our declaration blocks which elements they should be applied to, we need to prefix each declaration block with a **Selector** -- a pattern that matches some elements on the page.

The selector plus the declaration block is called a **Ruleset** (aka **Rule**).

### Element Selector
**Element Selector** is a case-insensitive match between the selector name and a given HTML element name.

```
div {
    color: black;
}
```

### Class Selector (.)
The **Class Selector** consists of a dot followed by a class name.

```
.highlighted-box {
    font-weight: bold;
}
```

### ID Selector (#)
The **ID Selector** consists of a hash symbol, followed by the ID name of a given element. 

An ID name must be unique in the document. Behaviors regarding duplicated IDs are unpredictable on different Internet browsers.

```
#brand {
    margin-top: 20px;
}
```

### Universal Selector (*)
The **Universal Selector** allows selecting all elements in a page.

Using it in large web pages can have an impact on performance because web pages can be displayed slower than expected.

```
* {
    margin: 0;
    padding: 0;
}
```

## Combinators
Combinators allow us to combine multiple selectors together to select elements inside other elements, or adjacent to other elements.

### Child Selector (>)
Select an element that is an immediate child of another element.

```
div > p {
    font-weight: bold;
}
```

### Descendant Selector (space)
Select an element nested somewhere inside another element (not necessarily a direct descendant; it could be a grandchild, for example).

```
div p {
    font-weight: bold;
}
```

### Adjacent Sibling Selector (+)
Select an element that is an immediate sibling of another element at the same level in the hierarchy.

```
div + p {
    font-weight: bold;
}
```

### General Sibling Selector (~)
Select all elements that are siblings of another element at the same level in the hierarchy.

```
div ~ p {
    font-weight: bold;
}
```

## Attribute Selector
Attribute selectors match elements based on their attributes and attribute values.

The syntax consists of square brackets ([]) containing an attribute name followed by an optional condition to match against the value of the attribute.

- `[attr]` selects all elements with the attribute `attr`, whatever its value.
- `[attr="val"]` selects all elements with the attribute `attr` having `val` as its value.
- `[attr~="val"]` selects all elements with the attribute `attr`, but only if the value `val` is one of a **space-separated list of values** contained in `attr`'s value.
- `[attr|="val"]` selects all elements with the attribute attr for which the value is exactly `val`, or followed by a hyphen(-) (For `[attr|="val"]` to work in IE8 and earlier, a `DOCTYPE` must be declared.).
- `[attr^="val"]` selects all elements with the attribute `attr` for which the value starts with `val`.
- `[attr$="val"]` selects all elements with the attribute `attr` for which the value ends with `val`.
- `[attr*="val"]` selects all elements with the attribute `attr` for which the value contains the string `val`. Unlike `[attr~=val]`, this selector doesn't treat spaces as value separators but as part of the attribute value.
