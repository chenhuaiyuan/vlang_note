## 注解(attribute)

V语言可以针对结构体,结构体字段,函数/方法进行注解

注解的格式统一是:[注解名] 或 [注解名:注解扩展内容]

### 编译器内置注解

#### 结构体注解

结构体注解统一放在结构体定义前

- [typedef]

  参考:[结构体章节](struct.md)
  
- [heap]

  参考:[结构体章节](struct.md)

#### 结构体字段注解

结构体字段注解统一放在字段定义后

- [required]

  参考:[结构体章节-字段注解](struct.md)
  
- [json]

  参考:[json章节](json.md)
  
- [skip]

  参考:[json章节](json.md)
  
- [row]

  参考:[json章节](json.md)

#### 函数注解

函数注解统一放在函数定义之前

- [deprecated]

  参考:[函数章节](fn.md)
  
- [inline]

  参考:[函数章节](fn.md)

- [live]

  参考:[函数章节](fn.md)

- [unsafe]

  参考:[unsafe章节](unsafe.md)

- [trusted]

  参考:[unsafe章节](unsafe.md)
  
- [if debug]

  这个注解表示该函数只有在编译时加上了-d 调试模式的时候,才会被编译生成,并且可以调用

  ```v
  [if debug]
  fn foo() {
  }
  ```

- [windows_stdcall]

  这个注解只能用于Win32 API,如果需要传递回调函数的时候使用
  
  ```v
  [windows_stdcall]
  fn C.DefWindowProc(hwnd int, msg int, lparam int, wparam int)
  ```

- [console]

  这个注解只能用在main函数前,导入了图形库模块(比如gg,ui)后,命令行窗口就不再显示了,查看不到命令行输出,加上这个注解,命令行窗口就会出现

  ```v
  [console]
  fn main() {}
  ```

### 自定义注解

实际上除了编译器内置的注解外,结构体,函数,枚举的定义者可以增加各种自定义注解,然后自己解析,自己使用

注解的扩展性还是比较灵活的

目前结构体注解和结构体字段注解,已经可以通过$for编译时反射来获取所有的注解内容,具体内容可以参考:[编译时反射章节](crossplatform.md)

```v
[testing]
struct StructAttrTest {
	foo string
	bar int
}

[testing]
struct PubStructAttrTest {
	foo string
	bar int
}

[testing]
enum EnumAttrTest {
	one
	two
}

[testing]
enum PubEnumAttrTest {
	one
	two
}

[attrone]
[attrtwo]
enum EnumMultiAttrTest {
	one
	two
}

[testing]
fn fn_attribute() {
}

[testing]
fn pub_fn_attribute() {
}

[attrone]
[attrtwo]
fn fn_multi_attribute() {
}

[attrone]
[attrtwo]
fn fn_multi_attribute_single() {
}

```

