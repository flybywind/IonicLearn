## index.html

### 入口：`ion-nav-view`
当用户浏览app时，Ionic可以跟踪浏览历史，同时可以正确的使用transition样式进入/退出子视图。另外，使用Ionic的浏览系统，可以操纵多个浏览历史，比如每个tab都可以有自己的浏览历史。

Ionic使用AngularUI Router来组织不同states（状态），跟`$router`服务类似，你可以使用URL来控制视图。但是，AngularUI Router提供一种更强大的状态管理器，每个状态都可以命名，可以相互嵌入，可以和其他视图并行显示，同时每个位置可以根据条件，用不同的模板渲染。另外，状态不一定非要和URL绑定，数据可以推入每个state以实现更多灵活性。

指示符`ionNavView`用来在你的app中渲染模板，每个模板对应一个状态。每个状态通常映射为一个url，每个状态通过程序定义。具体使用可以参考`angular-ui-router`的文档，注意使用时需要把`ui-view`换成`ion-nav-view`

默认情况下，ui-router会在父模板里寻找ion-nav-view插入模板，如果是根目录，就是index.html

### 主菜单 menu.html

#### ion-side-menus：

作用：用来容纳主体内容和侧边栏菜单的容器。用户可以在主体内容中向右滑动获得菜单选项。
用法：一个`<ion-side-menus>`后面必须至少跟着2个元素：`<ion-side-menu-content>`用来显示中间内容，以及一个或多个`<ion-side-menu>`用来存放左/右边栏。


#### ion-header-bar

在某些内容上面增加一个固定的bar。

如果使用了class ‘bar-subheader’ 会成为一个二级bar，位置稍低。

#### ion-nav-buttons

在ionView的ionNavBar里面，可以使用ion-nav-buttons设置多个按钮。每个view-template都可以用它设置自己的nav-bar，覆盖父模板中定义的默认导航栏。

button的位置根据side属性指定，如果`side="primary"`，通常会放在左边，如果`side="secondary"`，则放在右边，视设备情况而定。比如，在iOS上，primary button是放在左边， secondary右边，title中间；但是在Android设备上，两个button都会放在右边，同时title放左边。

基于此，使用primary和secondary是比较推荐的用法，但是如果要求button必须固定在左侧/右侧，也可以使用left、right指定side属性。

### $stateProvider参数说明：

[$stateProvider.state(stateName, stateConfig)](
https://github.com/angular-ui/ui-router/wiki/Quick-Reference#stateprovider-1)

#### `stateName`

string类型，表示唯一的状态名，如果是子状态，用点号连接。

#### `stateConfig`

object类型，包含如下有用属性：

##### template, templateUrl, templateProvider

和模板相关的3歌配置：

`template` HTML内容字符串，或者一个返回HTML字符串内容的函数

`templateUrl` www目录下的模板url地址，或者一个返回url地址的函数

`templateProvider` Function, 返回HTML内容字符串

##### controller, controllerProvider

和状态成对出现的controller。

`controller` 函数或者字符串表示的函数名。

`controllerProvider` 一个可以注入依赖的Function ，返回实际的controller函数或者函数名。

##### resolve

A map of dependencies which should be injected into the controller

resolve Object

keys - name of dependency to be injected into controller
factory - {string|function} If string then it is alias for service. Otherwise if function, it is injected and return value it treated as dependency. If result is a promise, it is resolved before its value is injected into controller

##### url

A url with optional parameters. When a state is navigated or transitioned to, the $stateParams service will be populated with any parameters that were passed.

[see more url routing](https://github.com/angular-ui/ui-router/wiki/URL-Routing)

##### params

A map which optionally configures parameters declared in the url, or defines additional non-url parameters. Only use this within a state if you are not using url. Otherwise you can specify your parameters within the url. When a state is navigated or transitioned to, the $stateParams service will be populated with any parameters that were passed.

`params` Object

Learn more about parameters (examples are shown in url form, but they work just the same here)

##### views

使用view属性在一个属性内设置多视图。如果不需要可以不设置。

> Tip: 嵌入式的view比并列的view更方便

`views` Object

keys - {string} name of ui-view，用key表示name属性，和`ion-nav-view`中的`name`属性对应。

view config - {object} view configuration object，key对应的值，可以用来设置该name的模板和controller。[Learn more about multiple named views
](https://github.com/angular-ui/ui-router/wiki#the-simplest-form-of-state)

##### abstract

state是否为抽象的，如果是，那么这个state永远不能被激活。常用来给子state设置公共视图、属性等。
`abstract` Boolean - (default is false)

##### onEnter, onExit

Callback functions for when a state is entered and exited. Good way to trigger an action or dispatch an event, such as opening a dialog.

onEnter Function, injected including resolves
onExit Function, injected including resolves
Learn more about state callbacks

##### reloadOnSearch v0.2.5

Boolean (default true). If false will not retrigger the same state just because a search/query parameter has changed. Useful for when you'd like to modify $location.search() without triggering a reload.

##### data

Arbitrary data object, useful for custom configuration.
