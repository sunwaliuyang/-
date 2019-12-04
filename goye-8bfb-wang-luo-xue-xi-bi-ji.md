### 问题1.golang怎么建立一个一一映射，现在的映射map是可以多对一的是吧？

建立两个map互查

### 问题2. golang中new与make关键字的区别和使用场景

```
#源码信息 源码地址：go/src/builtin/builtin.go
// The make built-in function allocates and initializes an object of type
// slice, map, or chan (only). Like new, the first argument is a type, not a
// value. Unlike new, make's return type is the same as the type of its
// argument, not a pointer to it. The specification of the result depends on
// the type:
//	Slice: The size specifies the length. The capacity of the slice is
//	equal to its length. A second integer argument may be provided to
//	specify a different capacity; it must be no smaller than the
//	length. For example, make([]int, 0, 10) allocates an underlying array
//	of size 10 and returns a slice of length 0 and capacity 10 that is
//	backed by this underlying array.
//	Map: An empty map is allocated with enough space to hold the
//	specified number of elements. The size may be omitted, in which case
//	a small starting size is allocated.
//	Channel: The channel's buffer is initialized with the specified
//	buffer capacity. If zero, or the size is omitted, the channel is
//	unbuffered.
func make(t Type, size ...IntegerType) Type

// The new built-in function allocates memory. The first argument is a type,
// not a value, and the value returned is a pointer to a newly
// allocated zero value of that type.
func new(Type) *Type
```

new接受一个参数，这个参数是一个类型，不是一个值，在分配好内存后，返回一个执行该类型内存地址的指针，请注意new同时把分配的内存置为零，即该类型的零值。

new不常用，new在一些需要实例化接口的地方用的比较多，但是可以使用$a{}代替。

但是new与$A{}存在一些差别，差别在于$A{}显示执行堆分配。

make也是用于内存的分配，但是make值使用与channel、map、slice的内存创建，而且它返回的类型就是这三个类型本身，而不是他们的指针类型，因为这三个类型本就是引用类型

注意：channel、map、slice是引用类型，所以必须得初始化，但是不能置为零值，这个跟new不一样

```
#举例说明
package main
import 'fmt'
func main(){
    p := new([]int) // p==nil;len、cap为0
    fmt.Println(p)
    v := make([]int,10,50) //  v 类型map，len为10，cap为50
    fmt.Println(v)
    /*********输出内容
    * &[]
    * [0 0 0 0 0 0 0 0 0]
    *
    ***********/
    (*p){0} = 18 // panic:runtime error:index out of range,原因：p为空指针 nil，并且len、cap都是0
    v[1] = 18 //ok
}

```



### Go语言--逃逸分析





