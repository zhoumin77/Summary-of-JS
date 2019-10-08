# 不明白的内容

```js
$('.sub-nav-search .SearchBar').keydown(function(event) {
  if (event.keyCode == 13) {
    $('.nav-submit-btn').trigger('click')
  }
})

;(function(scope) {
  scope.getElement('button[type=submit]').addEvent('click', function(e) {
    if (scope.getElement('input').value.trim() === '') {
      e.stop()
    }
  })
})($('searchbar_<{$widgets_id}>'))
// trigger
// button[type=submit]
// e.stop()
// trim
// destroy
```
