# Swift 4.2语法规范

## 注释

一般情况下，_方法，协议等自定义的内容_ 需要写注释，_属性_ 在需要补充说明的情况下需要写注释。_系统方法_ 不需要写注释

### Xcode的document功能

_方法，类，协议，结构体_ 等，推荐使用Xcode自带的document功能进行注释。

* 使用方法：

1. 按住⌘点击_方法，类，协议，结构体_ 名，在弹出的菜单选择_Add Documentation_即可自动生成注释，如下图。![add](./pic/adddocument.PNG)
2. 光标在_方法，类，协议，结构体_ 定义那一行的情况下，使用快捷键 ⌃+⌘+/（可以自定义设置或者修改）

* 一般来说参数，返回值都需要明确注释以便日后维护。使用add document添加注释之后,按住⌥点击方法名，可以有明确的注释出现，如下图。
![show](./pic/showdocument.png)

* 示例

  ```swift
  /// 根据时间戳获取开课时间,精确到分
  /// - Parameter timestamp: 时间戳字符串
  /// - Returns: 格式为 ‘2020-03-03 21:00’
  func getLessonTimeWithTimestamp(timestamp:String?) -> String
  ```

![show](./pic/showdocument.png)

### 注释规范

* **注释必须及时更新或删除**

 在使用版本控制的情况下。无效的代码或者注释及时删掉，如果不确定代码以后有没有可能用到，提交时写好commit，保证在需要的时候能找回来即可。

 注释掉的代码，90%都不会再用到。

* 注释的作用是解释“为什么这么做”，而不是“做了些什么”

  * 示例：
  * 做了些什么（不推荐）
  ![what](./pic/whatcomment.png)
  * 为什么这么做（推荐）
  ![why](./pic/whycomment.png)

* 少使用`/* ... */`，尽可能地用`//`或`///`代替。[为什么](https://stackoverflow.com/questions/61022236/why-the-need-to-avoid-c-style-comments-in-swift)

## 命名规范

* 清晰的优先级是高于简洁的
* classes, structures, enumerations and protocols 等类型名字以首字母大写驼峰命名。变量、方法名以小写驼峰方式命名，不要使用下划线
* 缩写和简写应该要尽量避免，遵守苹果命名规范，缩写和简写中的所有字符大小写要一致。
* 根据规则命名而不是根据类型命名
  * 推荐

    ```Swift
    var greeting = "Hello"
    protocol ViewController {
    associatedtype ContentView : View
    }
    class ProductionLine {
    func restock(from supplier: WidgetFactory)
    }
    ```

  * 不推荐

    ```Swift
    var string = "Hello"
    protocol ViewController {
      associatedtype ViewType : View
    }
    class ProductionLine {
      func restock(from widgetFactory: WidgetFactory)
    }
    ```

* 不要有拼写错误，发现后立刻改过来，方便以后全局搜索

## 代码结构

* 多使用extenion进行模块或者功能拆分
* 多使用 `// MARK: -`
* 减少无用的空行跟空格

## 协议相关

* 在extension中遵循需要方法实现的协议

  * 推荐

    ```swift
    class MyViewController: UIViewController {
    // class stuff here
    }

    // MARK: - UITableViewDataSource
    extension MyViewController: UITableViewDataSource {
    // table view data source methods
    }

    // MARK: - UIScrollViewDelegate
    extension MyViewController: UIScrollViewDelegate {
    // scroll view delegate methods
    }
    ```

  * 不推荐

    ```swift
    class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
        // all methods
    }
    ```

* 创建协议前，先考虑是不是有先有协议可以进行扩充