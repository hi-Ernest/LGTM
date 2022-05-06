# 怎么写比较好的单测 - 美观且实用

> go自带生成冗余的unitTesting长且不美观，期望实际单元测试，可以实现例如每次对代码某处进行改动的后，只需要run一遍就能把所有之前的单测数据跑一遍，校验改动是否引入新错误的影响，降低代码bug
>
> 做开源poj 发现某包：go get github.com/pingcap/check
>
> 封装好可开装直接使用，case如下，stdout简洁明了，体验不错

```go
package tablecodec

import (
	. "github.com/pingcap/check"
)

func TestT(t *testing.T) {
	//前置初始化依赖
    InitDB()
    InitConsumer()
    //运行下方结构体所有方法（即单测-包含的所有测试用例）
	TestingT(t)
}

var _ = Suite(&testTableCodecSuite{})

type testTableCodecSuite struct{}

//直接定义和实现该结构体方法，即可
func (s *testTableCodecSuite) TestTableCodec(c *C) {
	ctx := context.Background()
    req := &xxxRequest{}
    resp, err := xxxMethod(cxt, req)
    //断言是否为nil
	c.Assert(err, IsNil)
	//c.Assert(h, Equals, int64(2))
	//c.Assert(indexID, Equals, int64(math.MaxUint32))
	//c.Assert(isRecordKey, IsFalse)
}


func (s *testTableCodecSuite) TestCreateOrderV2(c *C) {
	ctx := context.Background()
    req := &xxxRequestV2{}
    resp, err := xxxMethodV2(cxt, req)
    //断言是否为nil
	c.Assert(err, IsNil)
	//c.Assert(h, Equals, int64(2))
	//c.Assert(indexID, Equals, int64(math.MaxUint32))
	//c.Assert(isRecordKey, IsFalse)
}


```

stdout 标准化输出

![](https://raw.githubusercontent.com/hi-Ernest/imgbed/master/API%20server%20listening%20at%20127.0.0.162392.png)

![](https://raw.githubusercontent.com/hi-Ernest/imgbed/master/Pasted%20Graphic%201.png)