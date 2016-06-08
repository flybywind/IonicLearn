## index.html

### 入口：`ion-nav-view`
当用户浏览app时，Ionic可以跟踪浏览历史，同时可以正确的使用transition样式进入/退出子视图。另外，使用Ionic的浏览系统，可以操纵多个浏览历史，比如每个tab都可以有自己的浏览历史。

Ionic使用AngularUI Router来组织不同states（状态），跟`$router`服务类似，你可以使用URL来控制视图。但是，AngularUI Router提供一种更强大的状态管理器，每个状态都可以命名，可以相互嵌入，可以和其他视图并行显示，同时每个位置可以根据条件，用不同的模板渲染。另外，状态不一定非要和URL绑定，数据可以推入每个state以实现更多灵活性。

指示符`ionNavView`用来在你的app中渲染模板，每个模板对应一个状态。每个状态通常映射为一个url，每个状态通过程序定义。具体使用可以参考`angular-ui-router`的文档，注意使用时需要把`ui-view`换成`ion-nav-view`

默认情况下，ui-router会在父模板里寻找ion-nav-view插入模板，如果是根目录，就是index.html

### $stateProvider参数说明：

[$stateProvider.state(stateName, stateConfig)](
https://github.com/angular-ui/ui-router/wiki/Quick-Reference#stateprovider-1)

#### `stateName`

string类型，表示唯一的状态名，如果是子状态，用点号连接。

#### `stateConfig`
