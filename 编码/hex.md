## Hex 编码

### 编码原理
Hex编码就是把一个8位的字节数据用两个十六进制数展示出来，编码时，将8位二进制码重新分组成两个4位的字节，其中一个字节的低4位是原字节的高四位，另一个字节的低4位是原数据的低4位，高4位都补0，然后输出这两个字节对应十六进制数字作为编码。Hex编码后的长度是源数据的2倍

```
ASCII码：A (65)
二进制码：0100_0001
重新分组：0000_0100 0000_0001
十六进制：        4         1
Hex编码：41
```

### Go使用
Golang 标准库的使用
```
func main() {
	src := []byte("48656c6c6f20476f7068657221")

	//解码
	dst := make([]byte, hex.DecodedLen(len(src)))
	n, err := hex.Decode(dst, src)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Printf("解码 %s\n", dst[:n])

	//编码
	sdst := make([]byte, hex.EncodedLen(len(dst[:n])))
	hex.Encode(sdst, dst[:n])

	fmt.Printf("编码 %s\n", sdst)
}
```
### Go实现

编码的实现很简单，高位用右移操作，低位用或操作，高位在前，低位在后
```
func Encode(dst, src []byte) int {
	j := 0
	for _, v := range src {
		dst[j] = hextable[v>>4]
		dst[j+1] = hextable[v&0x0f]
		j += 2
	}
	return len(src) * 2
}
```

解码的实现使用了一点小技巧，hextable记录了16进制的，fromHexChar计算高位和低位的ASCII值，再拼接起来。
```
const hextable = "0123456789abcdef"

func Decode(dst, src []byte) (int, error) {
	i, j := 0, 1
	for ; j < len(src); j += 2 {
		a, ok := fromHexChar(src[j-1])
		if !ok {
			return i, InvalidByteError(src[j-1])
		}
		b, ok := fromHexChar(src[j])
		if !ok {
			return i, InvalidByteError(src[j])
		}
		dst[i] = (a << 4) | b
		i++
	}
	if len(src)%2 == 1 {
		// Check for invalid char before reporting bad length,
		// since the invalid char (if present) is an earlier problem.
		if _, ok := fromHexChar(src[j-1]); !ok {
			return i, InvalidByteError(src[j-1])
		}
		return i, ErrLength
	}
	return i, nil
}

// fromHexChar converts a hex character into its value and a success flag.
func fromHexChar(c byte) (byte, bool) {
	switch {
	case '0' <= c && c <= '9':
		return c - '0', true
	case 'a' <= c && c <= 'f':
		return c - 'a' + 10, true
	case 'A' <= c && c <= 'F':
		return c - 'A' + 10, true
	}

	return 0, false
}
```



### 参考

[Hex编码](https://www.jianshu.com/p/57c4e8d3f035)
