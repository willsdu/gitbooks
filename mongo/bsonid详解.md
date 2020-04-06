# mongo bsonid 详解

本文将用bsonid=5a17b9d9ab102555b9c38874讲解

## bsonid的结构
bsonid是一个12字节的值，前4个字节是unix时间戳的秒数，接着是三字节的机器码，然后是2字节的PID，最后是3个字节的增量
```
BSONID  0-1-2-3---4-5-6---7-8---9-10-11
释义    time     machine  pid     inc
例子    5a17b9d9 ab1025   55b9    c38874
```
### 时间戳
前4位是一个unix的时间戳，精确到秒。是一个int类别，一共四个字节，转换为16进制，共8个字符。例子中的字符串"5a17b9d9"转为10进制是1511504345，也就是北京时间"2017/11/24 14:19:5"

1. 隐藏了文档的创建时间，ObjectId大致会按照插入进行排序
2. 记录了插入该记录的时候，该服务器的时间。
3. 这个值并不是十分的重要，只要能区别就好


### 机器ID
4字节的时间戳后面是3个自己的机器码，区别不同的服务器产生的bsonid。golang的mongo驱动"gopkg.in/mgo.v2/bson"的实现如下
```
func readMachineId() []byte {
	var sum [3]byte
	id := sum[:]
	hostname, err1 := os.Hostname()
	if err1 != nil {
        //如果找不到hostname就选择随机字数值
		_, err2 := io.ReadFull(rand.Reader, id)
		if err2 != nil {
			panic(fmt.Errorf("cannot get hostname: %v; %v", err1, err2))
		}
		return id
	}
	hw := md5.New()
    //对hostname MD5，取前三个字节
	hw.Write([]byte(hostname))
	copy(id, hw.Sum(nil))
	return id
}
```

### PID
机器码后面的是两个字节的进程ID，取进程ID的最后两个字节16位, 进程ID一般最大16位够描述了。
```
b[7] = byte(processId >> 8)
b[8] = byte(processId)
```


### 增量
增量也就是一个自动增加的计数器。允许256的3次方等于16777216条记录的唯一性，"gopkg.in/mgo.v2/bson"的实现如下，程序会在初始化的时候给给出一个随机的初始值，之后的增量在此值上增加。
```
var objectIdCounter uint32 = readRandomUint32()

// readRandomUint32 returns a random objectIdCounter.
func readRandomUint32() uint32 {
	var b [4]byte
	_, err := io.ReadFull(rand.Reader, b[:])
	if err != nil {
		panic(fmt.Errorf("cannot read random object id: %v", err))
	}
	return uint32((uint32(b[0]) << 0) | (uint32(b[1]) << 8) | (uint32(b[2]) << 16) | (uint32(b[3]) << 24))
}

...

i := atomic.AddUint32(&objectIdCounter, 1)
b[9] = byte(i >> 16)
b[10] = byte(i >> 8)
b[11] = byte(i)

...

```


## 参考
[MongoDB中ObjectId的误区，以及引起的一系列问题](https://blog.csdn.net/xiamizy/article/details/41521025)
[http://bsonspec.org/](http://bsonspec.org/)