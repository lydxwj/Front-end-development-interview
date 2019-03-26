# angular

## 1.angular路由

```jsx
var App = angular.module('App', ['ngRoute']);    
//3 配置路由模块，使其正常工作  
App.config(['$routeProvider', function ($routeProvider) {  	
  $routeProvider.when('/index', {  
    	// template: '<h1>index Pages!</h1>',  
   	 	templateUrl: './abc.html'  
  })  
  .when('/introduce', {  
 	 	template: '<h1>introduce Pages!</h1>'  
  })  
  .when('/contact', {  
    	// template: '<h1>contact US Pages!</h1>',  
    	templateUrl: './contact.html',  
        controller: 'ContactController' // 定义控制器  
  })  
  .when('/list', {  
      templateUrl: './list.html', // 视图模板  
      controller: 'ListController' // 定义控制器  
  })  
  .otherwise({  
      redirectTo: '/index'  
  });  
}]);  
```

### 详情请参考:

http://blog.csdn.net/u011301203/article/details/53236671

## 2.”脏“查询什么时候触发

- #### controller初始化的时候

- #### 所有以ng-开头的事件爱你执行后

- #### 手动的触发脏检查：$apply仅仅只是进入angular context，然后通过$digest触发脏检查

### 详情请参考:

http://www.cnblogs.com/liuyanan/p/4935652.html

http://www.cnblogs.com/likeFlyingFish/p/6183630.html

http://www.webnpm.com/60.html