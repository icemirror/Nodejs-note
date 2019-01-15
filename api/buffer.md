## Buffer

- Buffer 类用于在 **TCP 流**或**文件系统**操作等场景中处理字节流
- Buffer实例类似整数数组, 大小固定
- 在V8堆外分配物理内存
- Buffer是一个全局变量, 可以不用require引用

```
// 创建一个长度为10, 且用1填充的buffer
const buf1 = Buffer.alloc(10, 1)

// 创建包含具体值的buffer
const buf2 = Buffer.from([1, 2, 3])

// 也可以用string
const buf3 = Buffer.from('test', 'utf8')

// 创建一个不安全的buffer, 不安全的原因在于,以这种方式创建出来的
// buffer的内存是未经过初始化的, 也许带有一些数据.
const buf4 = Buffer.allocUnsafe(10)

```

### Buffer.byteLength

```
// buffer的单字节长度
const buf1 = Buffer.byteLength('test') // => 4
const buf2 = Buffer.byteLength('测试') // => 6
```

### Buffer.isBuffer

```
// 判断一个数据是否为buffer

const buf1 = Buffer.isBuffer({}) // => false
const buf2 = Buffer.isBuffer(Buffer.from([1, 2, 3])) // => true
```

### Buffer.concat

```
// 合并buffer数组
const buf1 = Buffer.from('Its')
const buf2 = Buffer.from('a')
const buf3 = Buffer.from('test')

const buf = Buffer.concat(buf1, buf2, buf3)

console.log(buf.toString()) // => Its a test
```

### Buffer.length

```
// 返回buffer的实际物理长度
const buf = Buffer.from('this is a test!')
console.log(buf.length) // => 15

const buf2 = Buffer.alloc(10) // 默认填充0
buf2[0] = 2

console.log(buf2.length) // => 10

const buf3 = Buffer.allocUnsafe(10) // 无默认填充
console.log(buf3.length) // => 10

```

### Buffer.fill

```
// 填充buffer
const buf = Buffer.allocUnsafe(10)
// fill(value, offset, end, encoding)
console.log(buf.fill(10, 2, 6)) // => <Buffer 00 00 0a 0a 0a 0a ff ff 00 00>
```

### Buffer.equals

```
// 比较两个buffer的内容是否一致
const buf = Buffer.from('test')
const buf2 = Buffer.from('test')
const buf3 = Buffer.from('test!')

console.log(buf.equals(buf2)) // => true
console.log(buf2.equals(buf3)) // => false
```

### Buffer.entries / keys / lastIndexOf / indexOf ...

buffer也支持一些数组的方法, 原理是一样的.

### Buffer.copy 

buf.copy(target[, targetStart[, sourceStart[, sourceEnd]]]): 拷贝buf中的某个区域的数据到target中的某个区域

```
// 举一个处理中文乱码的例子

const buf = Buffer.from('中文字符串!')

for (let i = 0; i < buf.length; i += 5) {
    const b = Buffer.allocUnsafe(5)
    buf.copy(b, 0, i)
    console.log(b.toString())
}
// 中�
// �字�
// ��串
// !o

// 利用字符串解码器sting_decoder解决乱码
const StringDecoder = require('string_decoder').StringDecoder
const decoder = new StringDecoder('utf8')

const buf2 = Buffer.from('中文字符串!')

for (let i = 0; i < buf2.length; i += 5) {
    const b = Buffer.allocUnsafe(5)
    buf2.copy(b, 0, i)
    console.log(decoder.write(b))
}

// 中
// 文字
// 符串
// !
```