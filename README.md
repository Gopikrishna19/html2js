html2js
===

RT. html2js. 解决require tpl无法跨域的问题

简单使用示例:

test.html:

```html
<div id="i-am-a-id">
  <div class="i-am-a-class">
    i am test
  </div>
</div>
```

js:

```javascript
var fs = require('fs');
var html2js = require('../html2js');

var filename = 'test.html';

var html = fs.readFileSync(filename, 'utf8');

var mode = ['format', 'default', 'compress'];

var arr = [];

mode.forEach(
    function (val) {
        arr.push( '// ' + val );
        arr.push( html2js( html, {mode: val, wrap: true} ) );
    }
);

var output = arr.join('\n');
console.log(output);
fs.writeFile( filename + '.js', output );
```
output:
```javascript
// format
define(function () {
    return ''
    + '<div id="i-am-a-id">\n'
    + '  <div class="i-am-a-class">\n'
    + '    i am test\n'
    + '  </div>\n'
    + '</div>';
});
// default
define(function () { return '<div id="i-am-a-id">\n  <div class="i-am-a-class">\n    i am test\n  </div>\n</div>';});
// compress
define(function () { return '<div id=\"i-am-a-id\"><div class=\"i-am-a-class\">i am test</div></div>';});
```
