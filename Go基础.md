# Go  Modules



### GO111MODULE

- GO111MODULE=off
  寻找依赖包的方式将会沿用旧版本那种通过vendor目录或者GOPATH模式来查找。

> 当modules 功能启用时，依赖包的存放位置变更为`$GOPATH/pkg`，允许同一个package多个版本并存



设置好GO ROOT  和 GO PATH，开启 IDE 的GO Modules 

![image-20210530112219522](C:\Users\mi\AppData\Roaming\Typora\typora-user-images\image-20210530112219522.png)

```go
go mod init downExam
go run main.go
```

配置设置好后，运行代码引入包会自动变成绿色

![image-20210530112443401](C:\Users\mi\AppData\Roaming\Typora\typora-user-images\image-20210530112443401.png)







接受数据库返回的批量数据用**切片**

> var questionLibrary []QuestionLibrary   一定需要加 []

```go

//题库分类信息
type QuestionLibrary struct {
	Id       string
	Name     string
	ParentId string
}
// 批量查询时，需要加 [],返回的是切片
var questionLibrary []QuestionLibrary
// Map 作为查询条件
db.Where(map[string]interface{}{"app_id": appId, "state": 0}).Find(&questionLibrary)

```



**map** 形式存储 需要通过索引查询的数据，key 值是字符串

```go

//题库分类信息
type QuestionLibrary struct {
	Id       string
	Name     string
	ParentId string
}
//定义一个map,以key-value 形式存储数据
libraryMap := make(map[string]QuestionLibrary)
// 导出文件名拼接
for _, library := range questionLibrary {
    libraryMap[library.Id] = library
}	
```



**map 二维数组**使用，map 值类型是一个切片

```go
optionMap := make(map[string][]Option)
for _, option := range optionList {
   //二维数组
   optionMap[option.QuestionId] = append(optionMap[option.QuestionId], option)
}
```



**切片 二维数组**

```go
type ExcelSheetData struct {
   SheetName string
   SheetData [][]string
}

sheet1 := [][]string{}
sheet1_row1 := []string{
   "题目题干(必填)", "选项A", "选项B", "选项C", "选项D", "选项E", "选项F", "选项G",
   "正确答案（必填）", "答案解析(选填)"}
sheet1 = append(sheet1, sheet1_row1) //第一行
```



**json** 处理，**一维数组**，key 是int 类型

```go
//todo 这种好像只能用 切片接受，map 无法实现
var jsonStr []string
json.Unmarshal([]byte(question.CorrectAnswer), &jsonStr)
```



方法直接返回一个数据

```go
func A2Z() []string {
   return []string{"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O",
      "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"}
}
column_map := A2Z()
column_map[index]
```



map 中定义一个值

```go
//map 中初始化一个值，需要写 key 和value
var abcMap = map[int]string{
	0:  "A",
	1:  "B",
	2:  "C",
	3:  "D",
	4:  "E",
	5:  "F"
}



//切片中初始化不需要指定key
var A2Z = []string{
	"A", "B", "C", "D", "E", "F", "G", "H"
}
```





