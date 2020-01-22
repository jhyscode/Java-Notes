# MVC

**MVC模式**（Model–view–controller）是[软件工程](https://zh.wikipedia.org/wiki/软件工程)中的一种[软件架构](https://zh.wikipedia.org/wiki/软件架构)模式，把软件系统分为三个基本部分：模型（Model）、视图（View）和控制器（Controller）。

MVC模式最早由[Trygve Reenskaug](https://zh.wikipedia.org/w/index.php?title=Trygve_Reenskaug&action=edit&redlink=1)在1978年提出，是[施乐帕罗奥多研究中心](https://zh.wikipedia.org/wiki/帕羅奧多研究中心)（Xerox PARC）在20世纪80年代为程序语言[Smalltalk](https://zh.wikipedia.org/wiki/Smalltalk)发明的一种软件架构。**MVC模式**的目的是实现一种动态的程序设计，使后续对程序的修改和扩展简化，并且使程序某一部分的重复利用成为可能。除此之外，此模式透过对复杂度的简化，使程序结构更加直观。软件系统透过对自身基本部分分离的同时也赋予了各个基本部分应有的功能。专业人员可以依据自身的专长分组：

- **控制器（Controller）**- 负责转发请求，对请求进行处理。

- **视图（View)** - 界面设计人员进行图形界面设计。

- **模型（Model)**- 程序员编写程序应有的功能（实现算法等等）、数据库专家进行数据管理和数据库设计(可以实现具体的功能)。

  <p align="center">
    <img  src="MVC.assets/ModelViewControllerDiagramZh-1578534943046.png">
  </p>

# 1.组件的互动

将应用程序划分为三种组件，模型 - 视图 - 控制器（MVC）设计定义它们之间的相互作用。

- **模型(Model)**     用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法。“ Model ”有对数据直接访问的权力，例如对数据库的访问。“Model”不依赖“View”和“Controller”，也就是说， Model 不关心它会被如何显示或是如何被操作。但是 Model 中数据的变化一般会通过一种刷新机制被公布。为了实现这种机制，那些用于监视此 Model 的 View 必须事先在此 Model 上注册，从而，View 可以了解在数据 Model 上发生的改变。（比如：[观察者模式](https://zh.wikipedia.org/wiki/观察者模式)（[软件设计模式](https://zh.wikipedia.org/wiki/软件设计模式)））
- **视图(View)**    能够实现数据有目的的显示（理论上，这不是必需的）。在 View 中一般没有程序上的逻辑。为了实现 View 上的刷新功能，View 需要访问它监视的数据模型（Model），因此应该事先在被它监视的数据那里注册。
- **控制器(Controller)**     起到不同层面间的组织作用，用于控制应用程序的流程。它处理事件并作出响应。“事件”包括用户的行为和数据 Model 上的改变。

# 2. 优点

在最初的JSP网页中，像[数据库](https://zh.wikipedia.org/wiki/数据库)查询语句(SQL query)这样的数据层代码和像[HTML](https://zh.wikipedia.org/wiki/HTML)这样的表示层代码是混在一起。虽然有着经验比较丰富的开发者会将数据从表示层分离开来，但这样的良好设计通常并不是很容易做到的，实现它需要精心地计划和不断的尝试。MVC可以从根本上强制性地将它们分开。尽管构造MVC应用程序需要一些额外的工作，但是它带给我们的好处是毋庸置疑的。

首先，多个 View 能共享一个 Model 。如今，同一个Web应用程序会提供多种用户界面，例如用户希望既能够通过浏览器来收发[电子邮件](https://zh.wikipedia.org/wiki/电子邮件)，还希望通过手机来访问[电子邮箱](https://zh.wikipedia.org/wiki/电子邮箱)，这就要求Web网站同时能提供[Internet](https://zh.wikipedia.org/wiki/Internet)界面和[WAP](https://zh.wikipedia.org/wiki/WAP)界面。在MVC设计模式中， Model 响应用户请求并返回响应数据，View 负责格式化数据并把它们呈现给用户，业务逻辑和表示层分离，同一个 Model 可以被不同的 View 重用，所以大大提高了代码的可重用性。

其次，Controller 是自包含（self-contained,指高独立内聚）的对象，与 Model 和 View 保持相对独立，所以可以方便的改变应用程序的数据层和业务规则。例如，把数据库从[MySQL](https://zh.wikipedia.org/wiki/MySQL)移植到[Oracle](https://zh.wikipedia.org/wiki/Oracle)，或者把[RDBMS](https://zh.wikipedia.org/wiki/RDBMS)数据源改变成[LDAP](https://zh.wikipedia.org/wiki/LDAP)数据源，只需改变 Model 即可。一旦正确地实现了控制器，不管数据来自数据库还是[LDAP](https://zh.wikipedia.org/wiki/LDAP)服务器，View 都会正确地显示它们。由于MVC模式的三个模块相互独立，改变其中一个不会影响其他两个，所以依据这种设计思想能构造良好的少互扰性的构件。

此外，Controller 提高了应用程序的灵活性和可配置性。Controller 可以用来连接不同的 Model 和 View 去完成用户的需求，也可以构造应用程序提供强有力的手段。给定一些可重用的 Model 、 View 和Controller 可以根据用户的需求选择适当的 Model 进行处理，然后选择适当的的 View 将处理结果显示给用户。

# 3. 评价、误解及适用范围

MVC模式在概念上强调 Model, View, Controller 的分离，各个模块也遵循着由 Controller 来处理消息，Model 掌管数据源，View 负责数据显示的职责分离原则，因此在实现上，MVC 模式的 Framework 通常会将 MVC 三个部分分离实现：

- Model 负责数据访问，较现代的 Framework 都会建议使用独立的数据对象 (DTO, POCO, POJO 等) 来替代弱类型的集合对象。数据访问的代码会使用 Data Access 的代码或是 ORM-based Framework，也可以进一步使用 Repository Pattern 与 Unit of Works Pattern 来切割数据源的相依性。
- Controller 负责处理消息，较高端的 Framework 会有一个默认的实现来作为 Controller 的基础，例如 Spring 的 DispatcherServlet 或是 ASP.NET MVC 的 Controller 等，在职责分离原则的基础上，每个 Controller 负责的部分不同，因此会将各个 Controller 切割成不同的文件以利维护。
- View 负责显示数据，这个部分多为前端应用，而 Controller 会有一个机制将处理的结果 (可能是 Model, 集合或是状态等) 交给 View，然后由 View 来决定怎么显示。例如 Spring Framework 使用 JSP 或相应技术，ASP.NET MVC 则使用 Razor 处理数据的显示。

也因为 MVC 模式强调职责分离，所以在发展 MVC 应用时会产生很多文件，在 IDE (集成开发环境) 不够成熟时它会是个问题，但在现代主流 IDE 都能使用类别对象的信息来组织代码编辑的情况下，多文件早已不是问题，而且 MVC 模式会要求开发者进一步思考应用程序的架构 (Application Architecture)，而非用大杂烩的方式开发应用程序，对于应用程序的生命周期以及后续的可扩展与可维护性而言有相当正面的帮助。另外，MVC 职责分离也带来了一个现代软件工程要求的重要特性：可测试性 (Testability)，MVC-based 的应用程序在良好的职责分离的设计下，各个部分可独立行使[单元测试](https://zh.wikipedia.org/wiki/单元测试)，有利于与企业内的自动化测试、[持续集成](https://zh.wikipedia.org/wiki/持續整合) (Continuous Integration) 与[持续发行](https://zh.wikipedia.org/w/index.php?title=持續發行&action=edit&redlink=1) (Continuous Delivery) 流程集成，减少应用程序改版部署所需的时间。

MVC 模式的应用程序的目的就是希望打破以往应用程序使用的大杂烩程序撰写方式，并间接诱使开发人员以更高的架构导向思维来思考应用程序的设计，因此对于一个刚入门的初学者来说，架构导向的思考会有一定的门槛，需要较多的实现与练习才能具备相应的能力，大多数的初学者还是较习惯于大杂烩式的程序撰写，所以可能会对 MVC 模式抱持着排斥或厌恶的心态，然而 MVC (或是其他的[Design Patterns](https://zh.wikipedia.org/w/index.php?title=Design_Patterns&action=edit&redlink=1)) 都是有助于应用程序长远的发展，虽然大杂烩式的程序也可以用来发展长生命周期的应用程序，但是相较于 MVC，大杂烩式的程序在可扩展性和可维护性 (尤其是可测试性) 上会远比 MVC 复杂很多，相反的，MVC 模式的应用程序是在初始开发时期必须先思考并使用软件架构，使得开发时期会需要花较多心力，但是一旦应用程序完成后，可扩展性、可维护性和可测试性反而会因为 MVC 的特性而变得容易。

因此，MVC 模式在已有众多优秀 Framework 的现代，早就已经没有不适合小型应用的问题，小型的应用还是可以由 MVC Framework 的应用来获取 MVC 的优点，同时它也能作为未来小型应用扩展到大型应用时的基础与入门砖。若一开始就想要做大型应用，那么 MVC 模式的职责分离以及要求开发的架构思考会更适合大型应用的开发。