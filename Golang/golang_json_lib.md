#go自带的json库为encoding/json

#对象转化为json
将对象转化为json的方法为`json.marshal()`, 其原型为`func Marshal(v interface{}) ([]byte, error)`
`接受任意类型的数据v, 将其转化为字节数组, 即json数据;`

类型转换
1. 布尔型-->布尔型;
2. `浮点型, 整型-->json里常规数字, 1.21-->1.21;`
3. 字符串以UTF8编码转化为Unicode字符串;
4. 数组和切片转化为json里的数组, []byte类转化为base64编码的字符串, slice零值转化为nil;
5. 结构体转化为json对象, 只有结构体里`以大写字母开头的可导出字段才会转化输出`, 可导出的对象会成为json对象的字符串索引;
6. 转化map类型时, `该类型必须是map[string]T`, 其中T是encoding/json支持的任意数据类型;

#json转化为对象
`func Unmarshal(data []byte, v interface{}) error`
将传入的data作为json解析, 并存储在v中, 其中v是任意类型(一定是`指针类型`)

Unmarshal的解析原则
例: json对象有一个"Foo"的索引, 则查找原则为:
1. 包含Foo的字段;
2. 名为Foo的字段;
3. 除了首字母`其他字母不分大小写`的名为Foo的字段(首字母必须大写);

当json的结构未知时, 遵循以下原则:
1. json中的布尔型转化为go的布尔型;
2. `数值转化为go的float`;
3. 字符串转化为string;
4. `json数组转化为[]interface{}`;
5. `json对象转化为map[string]interface{}`;
6. null值转化为nil;
* `encoding/json使用[]inteface{}和map[string]inteface{}来存储未知结构的数组或对象;`
