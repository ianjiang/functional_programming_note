### Tips: Function.apply

* build an array, first item will be the first paramter of the function
* use `Function.call(null, [paramtersArray])`

Example:

```javascript
function existy(x) { return x != null}

function cat() {
	var head = _.first(arguments);
    if (existy(head)) {
    	return [].concat.apply(head, _.rest(arguments));
    } else {
    	return [];
    }
}

function construct(head, tail) {
	return cat([head], _.toArray(tail));
}

function project(table, keys) {
	return _.map(table, function(obj) {
	    // construct(obj, keys): build paramter array
	    // equal to: _.pick(obj, keys);
    	return _.pick.apply(null, construct(obj, keys));
    })
}

var lib = [{title:'SICP', isbn:'1', ed:1},
		   {title:'SICP', isbn:'2', ed:2}];

var result = project(lib, ['title', 'isbn']);

console.log('result:', result)
console.log(_.pick({title:'SICP', isbn:'1', ed:1}, 'title'))

```
