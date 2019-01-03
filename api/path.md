## Path

> The path module provides utilities for working with file and directory paths

Path是用于处理文件和目录路径的模块, 在你的程序中引入path模块: 

```
const path = require('path')
```

- ### path.normalize(path)

path.normalize用于格式化指定路径为合法路径的方法.
```
// 用法
normalize (path) {
    /*
     * @param {String} path 需要被格式化的路径
     * @return {String} 被格式化后的路径
     **/
}

// 例子
const {normalize} = require('path')

console.log(normalize('/usr//local/bin')) // => /usr/local/bin
console.log(normalize('/usr/local/../bin)) // => /usr/bin
```
- ### path.join(path)

path.join用于路径拼接

```
// 用法
join ([...paths]) {
    /*
     * @param {String} ...path 路径序列
     * @return {String} 拼接后的路径
     **/
}
// 例子
const {join} = require('path')

console.log(join('/usr', 'local', 'bin/')) // => /usr/local/bin/
console.log(join('/usr', '../local', '/bin')) // => /local/bin
```
可以推测, join的方法应该也是调用了normalize的方法将拼接结果格式化的.

- ### path.resolve(path)

path.resolve用于将相对路径转换为绝对路径的方法.

```
// 用法
resolve ([...paths]) {
    /*
     * @param {String} ...path 路径序列
     * @return {String} 拼接后的路径
     **/
}
// 例子
const {resolve} = require('path')

console.log(resolve('./')) // => /Users/goodhome/Desktop/first-node
console.log(resolve('./', '../')) // => /Users/goodhome/Desktop
```

- ### path.basename path.extname path.dirname

```
// 用法
basename (path[,ext]) {
    /*
     * @param {String} path 路径
     * @param {String} ext [可选] 文件扩展名
     * @return {String} 路径的最后一部分
     **/
}
extname (path) {
    /*
     * @param {String} path 路径
     * @return {String} 文件扩展名
     **/
}
dirname (path) {
    /*
     * @param {String} path 路径
     * @return {String} 目录名称
     **/
}
// 例子
const {basename, extname, dirname} = require('path')

let filePath = '/usr/local/bin/test.txt'
console.log(basename(filePath)) // => test.txt
console.log(extname(filePath))  // => .txt
console.log(dirname(filePath))  // =>  /usr/local/bin
```
- ### path.parse path.format

path.parse用于将路径转换为一个对象, 这个对象包括了路径的重要属性(根目录, 目录名称, 文件名, 扩展名等...)); path.format则与parse作用相反

```
// 用法
parse (path) {
    /*
     * @param {String} path 路径
     * @return {Object} 路径重要属性组成的对象
     **/
}
format (pathObject) {
    /*
     * @param {Object} 路径重要属性组成的对象
     * @return {String} 格式化后的路径
     **/
}

// 例子
const {parse, format} = require('path')

parse('/usr/local/bin/test.txt');
// Returns:
// { base: 'test.txt',
//   dir: '/usr/local/bin',
//   ext: '.txt',
//   name: 'test',
//   root: '/' }

format({
    base: 'test.txt',
    dir: '/usr/local/bin',
    ext: '.txt',
    name: 'test',
    root: '/'
})
// => /usr/local/bin/test.txt
```
