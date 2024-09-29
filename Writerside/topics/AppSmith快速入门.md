# AppSmith 快速入门

> AppSmith 是一款开源的快速应用开发工具，允许你以最简单的方式快速创建 Web 和移动应用。

## 主要特性如下：

- **丰富的组件库**：AppSmith 包含一套丰富的组件库，用户可以通过简单的拖拽方式构建自己的应用界面。
- **强大的集成能力**：AppSmith 支持与包括数据库(例如MySQL, PostgreSQL等)、API、GraphQL 等资源进行集成，有效地提高了开发效率。
- **快速应用开发**：AppSmith 提供了便捷的操作方式，无论你是开发者还是非技术人员，都可以在短时间内搭建出属于自己的应用，大大缩短项目的上线周期。

## 如何搭建?

- 首先创建Amazon EC2新实例。
- 在“快速启动“页面中，点击浏览其他AMI。
- 在搜索框中输入“AppSmith”并选择"AWS Marketplace AMI"。
- 对于初学者，我们推荐选择community 版本
  ![appsmith-ec2-image](appsmith-ec2-image.png)
- EC2创建成功后，进入EC2详情中找到 公有地址。
- 接下来就可以通过输入公有地址在浏览器中访问并启用AppSmith了。

## 如何使用?

### 如何添加新用户

- 登陆后，点击网页右上角的三个点(设置菜单)
  ![appsmith-adduser1](appsmith-adduser1.png)
- 点击出现的“Members”选项
- 在打开的页面右上角点击“Add users”
- 添加新用户的邮箱和权限
  ![appsmith-adduser2](appsmith-adduser2.png)
- 最后通知该用户访问该网站并注册账号即可

### 使用教程

- 首页点击"Create New"创建新应用后进入编辑页
  ![appsmith-edit1](appsmith-edit1.png)
- 在左侧"Data"栏中,用户可以添加和管理数据源,并可以进行各类数据库的连接
  ![appsmith-edit2.png](appsmith-edit2.png)
- 在UI栏，用户可以选择各类UI组件，直接拖入中间编辑区即可
  ![appsmith-edit3.png](appsmith-edit3.png)
- 界面的每个组件都有各自的属性，例如位置、大小、颜色等等，用户可以使用js变量或者函数来定义。 示例格式如下

<code>{{backend_data.filiterData.data[0]}}</code>
![appsmith-edit4.png](appsmith-edit4.png)

- 需要注意的是，若使用函数作为属性时。每次调用函数会更新引用该函数的属性。如果不触发函数则会持续显示原有的值。
- 触发函数的方法包括 点击按钮、页面加载时执行、UI组件的回调等。

### 了解JS代码

- 在屏幕左上角找到JS按钮后，点击后可以新建JSObject。这个就相当于一个声明并创建的类。
- 然后可以在类中定义变量和函数，这些变量和函数也可以在外部引用
  ![appsmith-js1.png](appsmith-js1.png)
- 另外每个UI组件实际上也是一个对象。所以可以在JS代码中引用它们的属性。
  ![appsmith-js2.png](appsmith-js2.png)
- 事实上你也可以在JS中调用事先定义好的[Queries](#queries)，用于获取数据。
  ![appsmith-js3.png](appsmith-js3.png)
- 综上，AppSmith的JS就实现了数据库、UI、逻辑操作的无缝连接。

### 能力强大的Queries

> Queries就相当于数据库的查询语句，一个数据源可以创建多个Queries。Queries提供了丰富的查询选项，可以自定义查询参数，从而返回特定的数据集。

![appsmith-queries1.png](appsmith-queries1.png)

- 创建Queries
    - 在左侧"Data"菜单栏找到你的数据库，并点击旁边的"+”按钮创建一个新的Query。
    - 在打开的页面中输入你的查询代码。Queries支持各种如MySQL，PostgreSQL等常见的数据库查询语言。
    - 确认查询条件并保存。

- 使用Queries
    - 你可以在JS代码中引用你创建的Queries。每个Query都会返回一个对象，你可以使用该对象进行数据的解析和操作。

- 更新Queries
    - 当你的数据源更新时，你可以随时修改你的Queries以适应新的数据需求。
    - 每次修改Queries后，所有引用该Queries的代码会自动更新，保证数据的一致性。

- 删除Queries
    - 如果一个Queries已经不再使用，你可以选择删除它以保持你的项目的清洁和整洁。
    - 注意：删除Queries会影响到引用了该Queries的所有代码，所以请在考虑清楚后再进行删除。

通过灵活使用Queries，你可以更好地管理你的数据源，从而大大的提升你的开发效率。

