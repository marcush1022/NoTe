#STRING METHODS
`a string is a [read-only] slice of bytes`

`Original string`
str := "abcdefcdeh"
fmt.Printf("=> Type of str[1]: %T\n", str[1]) // uint8, `字符串元素的类型`;

`String to rune`
`str[index]获取的是字符byte, 需要首先将string转化为rune数组, 通过下标访问获取字符的unicode码，然后将unicode码转为字符串`;
fmt.Printf("=> strRune's type is: %T\n", strRune) // []int32, `rune数组元素的类型`;
fmt.Printf("=> string(strRune[1]): %v\n", string(strRune[1])) //b, `下标访问`;

`Contain and count of substring`
fmt.Println("=> strings.contains(str, cde): ", strings.Contains(str, "cde")) // true, `是否包含特定子串`;
fmt.Println("=> strings.count(str, cde): ", strings.Count(str, "cde")) // 2, `子串在原字符串中出现的次数`;
fmt.Println("=> strings.count(str, ): ", strings.Count(str, "")) // 11, `若子串为"", 则无论str为何值，均返回len(str)+1`;

`Fields`
strToSeparate := "abc cde fre" 
strSeparated := strings.Fields(strToSeparate)
fmt.Printf("=> strSeparated: %v, strSeparated[1]: %v\n", strSeparated, strSeparated[1])
// strSeparated: [abc cde fre], strSeparated[1]: cde
// 按空格(1或n个)分割字符串，判断是否是空格根据`unicode.IsSpace`, 若字符串只含有空格则返回空slice, `否则返回分割后的子串组成的slice`;

`ContainsRune`
var rune1 int32
rune1 = 'f'
fmt.Printf("=> containsRune(str, f): %v\n", strings.ContainsRune(str, rune1))
// `判断字符串中是否有unicode f`

`Index of substring`
fmt.Printf("=> index(str, cde): %v\n", strings.Index(str, "cde")) // index(str, cde): 2, `子串第一次出现的位置`;
fmt.Printf("=> lastIndex(str, cde): %v\n", strings.LastIndex(str, "cde")) // lastIndex(str, cde): 6, `子串最后一次出现的位置`;

`Repeat`
strForCopy := "bar"
strCopied := strings.Repeat(strForCopy, 3)
fmt.Printf("=> stringRepeat(strForCopy, 3): %v\n", strCopied) // barbarbar, `由已有子串重复构成新的字符串`;

`Replace with substr`
strForReplace := "barfoo the foobar is foobar"
fmt.Printf("=> strForReplace after replace(-1): %v\n", strings.Replace(strForReplace, "foobar", "barfoo", -1))
// barfoo the barfoo is barfoo
fmt.Printf("=> strForReplace after replace(1): %v\n", strings.Replace(strForReplace, "foobar", "barfoo", 1))
// barfoo the barfoo is foobar
`使用新子串替换字符串中的旧子串，并制定替换的数量, -1表示无限制`;

`Join`
strLeft := []string{"foobar", "is", "foobar"}
strRight := "BARFOO"
strHead := []string{"A", "A", "A", "A"}
strRear := "a"
fmt.Printf("=> connect strLeft and strRight: %v\n", strings.Join(strLeft, strRight)) // foobarBARFOOisBARFOOfoobar
fmt.Printf("=> connect strHead and strRear: %v\n", strings.Join(strHead, strRear)) // AaAaAaA
`返回的字符串为字符串数组和字符串的交错组合`;

`toLower and toUpper`
strMixesLowerAndUpper := "aAbBcC"
fmt.Printf("=> aAbBcC to lower: %v\n", strings.ToLower(strMixesLowerAndUpper)) // `全部转为小写`;
fmt.Printf("=> aAbBcC to upper: %v\n", strings.ToUpper(strMixesLowerAndUpper)) // `全部转为大写`;

`trim`
strForTrim := "foobar"
fmt.Printf("=> foobar to trim: %v\n", strings.Trim(strForTrim, "fr")) // ooba
`移除原字符串首尾的指定字符, return a string has leading and rear character removed`

`split`
strForSplit := "foo,bar,is,bar,foo"
fmt.Printf("=> foo,bar,is,bar,foo to split: %v\n", strings.Split(strForSplit, ",")) // [foo bar is bar foo]
`用给定子串分割原字符串，并返回string array`;


