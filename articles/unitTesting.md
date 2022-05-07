# 怎么写比较好的单测 - 美观且实用

> go自带生成冗余的unitTesting长且不美观，比较好的单元测试具有以下特性
>
> [Software Engineering at Google - Unit Testing](https://qiangmzsx.github.io/Software-Engineering-at-Google/#/zh-cn/Chapter-12_Unit_Testing/Chapter-12_Unit_Testing)
>
> 1. 使用简洁的代码，清晰的代码层级，高效Run单元测试（绝大多数的单元测试只需要一个 "when "和一个 "then "块）
>
> 2. 好的测试库可以帮助我们更容易写出/打印有用的失败信息
>
> 3. 与其为每个方法写一个测试，不如为每个行为写一个测试
>
> 4. 以被测试的行为进行命名测试
>
> 5. 在测试代码中，坚持使用直线代码而不是复杂的逻辑，并在测试更具描述性的时候考虑容忍一些重复
>
>    「遵循DAMP而不是DRY！」
>
>    DRY—“Don’t Repeat Yourself.” 
>
>    DAMP—that is, to promote “Descriptive And Meaningful Phrases.”
>
> 
>
> 增加个人目的：希望实现例如每次对代码某处进行改动的后，只需要run一个方法一遍就能把所有之前的单测跑一遍，校验改动是否对之前的单测数据兼容。
>
> 做开源poj 发现某测试包：go get github.com/pingcap/check
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