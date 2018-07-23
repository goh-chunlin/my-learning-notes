# Document Object Model (DOM) Related

## getElementById versus jQuery Selector

`document.getElementById('id')` returns a HTML DOM Object while `$('#id')` returns a jQuery Object that wraps the DOM object and provides jQuery methods.

We can also write `$(document.getElementById('id'))`, which will return a jQuery object and is equivalent to `$('#id')`. To get the underlying DOM object from a jQuery object, we need to write `$('#id')[0]`.

A benefit of using jQuery is that when a desired element, for example an element with id=`id` is not found, then doing `document.getElementById('id')` will return `null`, whereas the `$('#id')` returns a jQuery object that will be empty if no element with the id of `id` is matched. Returning `null` is not always a desired behavior because it may cause our code to throw **uncaught type error**.

Take note that, however, technically `document.getElementById('id')` is quite a bit faster than `$('#id')`. The speed difference depends on how we use it. If it just a single call to either one of them, there will hardly be any difference. If the call is made hundreds or thousands of times inside a loop or recursively or something, we might notice that jQuery selector is a bit slower.

Generally, `getElementById` is faster but with jQuery we can do a lot of things in an easy manner.
