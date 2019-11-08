## 快速使用

* 准备（运行一次即可）
  * 安装 `Python`, `C` 编译器
  * 运行 `install_mods.bat` 安装模块
* 答题模板生成(如何根据题目建立答题文件)
  - 在命令行运行（或 `clion` 终端） `python cptc.py 22`，将自动生成带有模板的 `P0022.h` 和 `P0022.cpp`，默认模板集成了必要的类的函数，以及作者和创建时间
* 答题文件组成
  - 所有答题类都包含 `generate` 函数， 用于生成测试变量，与 `LeetCode` 需要提交的函数对接
  - 所有的答题类继承 `problem.h` 中的 `Problem` 虚基类，`Problem` 定义了纯虚函数 `void run()`, 用来测试写的 `LeetCode` 要提交的函数
  - 所以补全 `generate` 与 `run`， 根据题目新建 `LeetCode` 的核心函数, `.h` 写定义 `.cpp` 写实现
* 本地运行
  - 每次运行 `main.cpp`, 运行时**修改 `main.cpp` 中题号**即可
* 提交到 `LeetCode`
  - 在命令行运行(Clion可以直接运行终端) `python trans.py 22`， 剪切板将会替换为第22题的答题代码，直接粘贴到 `LeetCode` 提交就行。也可以执行 `python trans.py` ，题号手动输入。
  - 目前测试没什么问题，不确保一定所有代码都能成功处理。注意有的地方可能会有冲突，比如题目中有定义链表结构的，但是LeetCode内部自己也定义了，会出现重复定义的情况，这种情况无法处理，请自行删除重复定义的部分。

## 编程框架(现在写的有点乱，以后再整理)

* 运行
  
  * 每次运行 `main.cpp`, 运行时修改题号即可
  
* 答题文件组成
  * 所有答题文件为 `C++` 类， 由形如 `P0001.h` 与 `P0001.cpp` 的两个文件组成
  * `P0001.h` 包含 `common.h` , `common.h` 中包含了大多数常用库文件
  * 所有答题类都包含 `generate` 函数， 用于生成测试变量，与 `LeetCode` 需要提交的函数对接
  * 所有的答题类继承 `problem.h` 中的 `Problem` 虚基类，`Problem` 定义了纯虚函数 `void run()`, 用来测试写的 `LeetCode` 要提交的函数
  
* 答题模板生成

  * 基础操作：在命令行运行 `python cptc.py 22`，将自动生成带有模板的 `P0022.h` 和 `P0022.cpp`，默认模板集成了必要的类的函数，以及作者和创建时间

  * 模板自定义：

    * 原理：读取 `config.yaml` 文件的配置信息, 将 `template.h` 和 `template.cpp` 中所有 `$配置名` 替换为配置的属性（注意一定要一行一个变量，目前不支持多级变量, 具体如下）

    * ```yaml
      author: a
      property1: b
      # 上面的是正确的
      
      property2:
      	property3: c
      # 上面的形式目前不支持，虽然Yaml语法是对的
      ```

    * 如何修改自定义模板（静态）：

      * 直接修改 `temlate.h` 和 `template.cpp` 
      
    * 如何添加动态配置（比如创建时间）：
    
      1. 在 `cptc.py` 中的 `add_other2config` 函数中按照范例添加新配置, 如`self.configs['property'] = 。。。`
      2. 在 `template.h` 或 `temlate.cpp` 中需要的位置写上 `$property`
      
    * 如何在 `cptc.py` 中调用配置信息：
    
      * 使用 `self.configs['配置名']`即可

* 提交（新，自动）
  * 在命令行运行(Clion可以直接运行终端) `python trans.py 22`， 剪切板将会替换为第22题的答题代码，直接粘贴到 `LeetCode` 提交就行。也可以执行 `python trans.py` ，题号手动输入。
  * 目前测试没什么问题，不确保一定所有代码都能成功处理。注意有的地方可能会有冲突，比如题目中有定义链表结构的，但是LeetCode内部自己也定义了，会出现重复定义的情况，这种情况无法处理，请自行删除重复定义的部分。
  
* 提交（旧，手动）
  
  * 复制 `P0001.h` 与 `P0001.cpp` 的内容，删去头文件，`generate` 函数（可不删，但会增加编译时间）, `run` 函数（可不删），删除 `run` 函数的 `override` 注解，修改类名为 `Solution`。

## 已解决题目

> 以前答的不在这个项目里的就不放进来了

1. P0019
2. P0022
3. P0039
4. P9946
5. P0047
6. P0048
7. P0055