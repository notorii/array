# notorii:array


## Installation

In a Meteor app directory:
```bash
meteor add notorii:array
```

## Usage

### notoriiArray.remove

Removes one or more items from an array

- @param {Array} arr1 The array to remove from

- @param {Number} from The index to remove (or remove starting from if removing more than one)

- @param {Number} [to] The index to remove up to. Pass in boolean false to not use this parameter (i.e. if want to use 'params' but not 'to')

- @param {Object} [params]

  - @param {Boolean} [modifyOriginal] True to modify the passed in array itself (thus no return value is needed) - this is better for performance but can lead to unexpected behavior since the original version is modified everywhere it's used. NOTE: this doesn't seem to be working 100% properly - the returned value IS correct and no '.copy' is used so still good for performance, BUT the original array is cut to smaller length and is wrong.

@return {Array} arr1 The new array with the appropriate element(s) removed

```js
var arr1 =[
  {_id:1, name:'Joe'},
  {_id:2, name:'Bob'},
  {_id:3, name:'Sally'},
  {_id:4, name:'Sue'},
  {_id:5, name:'Becky'}
];
var smallerArray =notoriiArray.remove(arr1, 1, false, {});    //can also just do 'notoriiArray.remove(arr1, 1);' if not using 'to' or 'params' parameters
```

### notoriiArray.findArrayIndex

Returns the index of an 2D []{} associative array when given the key & value to search for within the array. Like native javascript '.indexOf()' but for arrays of objects.
- @param {Array} array 2D array []{} to search

- @param {String} key Object key to check value against

- @param {Mixed} val To match key value against

- @param {Object} [params]

  - @param {Boolean} oneD True if it's a 1D array

@return {Number} The index of the element OR -1 if not found


```js
var arr1 =[
  {_id:1, name:'Joe'},
  {_id:2, name:'Bob'},
  {_id:3, name:'Sally'},
  {_id:4, name:'Sue'},
  {_id:5, name:'Becky'}
];
var index1 =notoriiArray.findArrayIndex(arr1, 'name', 'Bob', {});   //index1 will return 1 since the 2nd element (array index 1 since arrays are 0 indexed) is the one with 'Bob' in the 'name' field
```

### notoriiArray.sort2D

takes a multidimensional array & array index to sort by and returns the multidimensional array, now sorted by that array index

- @param {Array} arrayUnsorted 2D array []{} of objects to sort

- @param {Number} column Array index to sort by (note first one is 0)

- @param {Object} [params]

  - @param {String} [order] 'desc' for reverse order sort

@return {Array} sortedArray input array of objects []{} but now sorted

```js
var arr1 =[
  {_id:1, name:'Joe'},
  {_id:2, name:'Bob'},
  {_id:3, name:'Sally'},
  {_id:4, name:'Sue'},
  {_id:5, name:'Becky'}
];
var sortedArray =notoriiArray.sort2D(arr1, 'name', {});   //will now have array sorted by alphabetical order by name (i.e. Becky, Bob, Joe, Sally, Sue)
```