# Data Attributes in HTML5

## Data Attributes
Data Attributes allow us to store extra information on standard, semantic HTML elements without other hacks.

For example, given the following table.
```
<table>
  <thead>
    <tr>
      <th>#</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>  
      <td>
        <select class="status-dropdown">
          ...
        </select>
      </td>
    </tr>
    <tr>
      <td>2</td>  
      <td>
        <select class="status-dropdown">
          ...
        </select>
      </td>
    </tr>
    ...
    <tr>
      <td>n</td>  
      <td>
        <select class="status-dropdown">
          ...
        </select>
      </td>
    </tr>
  </tbody>
</table>
```

Now, let's say we want to show the original value of the dropdown in `alert` whenever the dropdown is updated, we can do so with the following JavaScript.

```
  var statuses = [];
  
  $('.container-status-dropdown').each(function (index) {
    statuses.push($(this).val());
  });
  
  function showOriginalValue(index) {
    alert(statuses[index]);
  }
```

Then we add the showOriginalValue function to each of the dropdowns in HTML as follows.
```
...
<tr>
  <td>n</td>  
  <td>
    <select class="status-dropdown" onchange='showOriginalValue(n);'>
      ...
    </select>
  </td>
</tr>
...
```

The way above actually can be simplified further with Data Attribute as follows.
```
...
<tr>
  <td>n</td>  
  <td>
    <select class="status-dropdown" data-ItemId="n" onchange='showOriginalValue(this);'>
      ...
    </select>
  </td>
</tr>
...
```
Then we can simplify our JavaScript code above as follows.
```  
function showOriginalValue(dropdown) {
  $(dropdown).data('itemid');
}
```
