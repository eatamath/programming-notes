## Angular JS Doc Notes

#### Basics

During application bootstrap, before AngularJS goes off creating all services, it configures and instantiates all providers. We call this the configuration phase of the application life-cycle. During this phase, services aren't accessible because they haven't been created yet.

Once the configuration phase is over, interaction with providers is disallowed and the process of creating services starts. We call this part of the application life-cycle the run phase.

##### $scope

定义

[Scope](https://docs.angularjs.org/api/ng/type/$rootScope.Scope) is an object that refers to the application model. It is an execution context for [expressions](https://docs.angularjs.org/guide/expression). Scopes are arranged in hierarchical structure which mimic the DOM structure of the application. Scopes can watch [expressions](https://docs.angularjs.org/guide/expression) and propagate events. 

- Scopes provide APIs ([$watch](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch)) to **observe model mutations**.
- Scopes provide APIs ([$apply](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$apply)) to **propagate any model changes** through the system into the view from outside of the "AngularJS realm" (controllers, services, AngularJS event handlers).
- Scopes can be **nested** to limit access to the properties of application components while providing access to shared model properties. Nested scopes are either "child scopes" or "isolate scopes". A "child scope" (prototypically) inherits properties from its parent scope. An "isolate scope" does not. See [isolated scopes](https://docs.angularjs.org/guide/directive#isolating-the-scope-of-a-directive) for more information.
- Scopes provide **context** against which [expressions](https://docs.angularjs.org/guide/expression) are evaluated. For example `{{username}}` expression is meaningless, unless it is evaluated against a specific scope which defines the `username` property.

数据绑定解析过程

**Scope is the glue between application controller and the view**. During the template [linking](https://docs.angularjs.org/guide/compiler) phase the [directives](https://docs.angularjs.org/api/ng/provider/$compileProvider#directive) set up [`$watch`](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$watch) expressions on the scope. The `$watch` allows the directives to be notified of property changes, which allows the directive to render the updated value to the DOM. 

Logically the rendering of `{{greeting}}` involves:

- retrieval of the scope associated with DOM node where `{{greeting}}` is defined in template. In this example this is the same scope as the scope which was passed into `MyController`. (We will discuss scope hierarchies later.)
- Evaluate the `greeting` [expression](https://docs.angularjs.org/guide/expression) against the scope retrieved above, and assign the result to the text of the enclosing DOM element.
-  When AngularJS evaluates `{{name}}`, it first looks at the scope associated with the given element for the `name` property. If no such property is found, it searches the parent scope and so on until the root scope is reached. In JavaScript this behavior is known as prototypical inheritance, and child scopes prototypically inherit from their parents. 

Retrieving Scopes from the DOM [pass]

Scope Events Propagation [pass]

![img](https://docs.angularjs.org/img/guide/concepts-scope-watch-strategies.png)

AngularJS modifies the normal JavaScript flow by providing its own event processing loop. This splits the JavaScript into classical and AngularJS execution context. Only operations which are applied in the AngularJS execution context will benefit from AngularJS data-binding, exception handling, property watching, etc...  An explicit call to $apply is needed only when implementing custom event callbacks, or when working with third-party library callbacks. 

![img](https://docs.angularjs.org/img/guide/concepts-runtime.png)

##### scope inheretence

 A scope can inherit from a parent scope, as in this example: 

```js
var parent = $rootScope;
var child = parent.$new();

parent.salutation = "Hello";
expect(child.salutation).toEqual('Hello');

child.salutation = "Welcome";
expect(child.salutation).toEqual('Welcome');
expect(parent.salutation).toEqual('Hello');
```



##### $location

```js
    .config(['$locationProvider', function($locationProvider) {
        $locationProvider.html5Mode({
            enabled: true,
            requireBase: false
        });
    }])
```

##### \$ngView & \$routeProvider

实现视图注入

[example]( https://docs.angularjs.org/api/ngRoute/directive/ngView )

##### $compile

ng-repeat存在顺序问题，解决方案：先展开 ng-repeat 然后重新 init parent

这里有个例子

```js
app.controller('MainCtrl', function($scope) {
  $scope.items1 = [1,2,3,4,5];
  $scope.items2 = [1,2,3,4,5,6,7,8,9,10];
})
.directive("owlCarousel", function() {
	return {
		restrict: 'E',
		transclude: false,
		link: function (scope) {
			scope.initCarousel = function(element) {
			  // provide any default options you want
				var defaultOptions = {
				};
				var customOptions = scope.$eval($(element).attr('data-options'));
				// combine the two options objects
				for(var key in customOptions) {
					defaultOptions[key] = customOptions[key];
				}
				// init carousel
				$(element).owlCarousel(defaultOptions);
				console.log($(element).owlCarousel);
			};
		}
	};
})
.directive('owlCarouselItem', [function() {
	return {
		restrict: 'A',
		transclude: false,
		link: function(scope, element) {
		  // console.log(scope);
		  // console.log(element);
		  // wait for the last item in the ng-repeat then call init
			if(scope.$last) {
				scope.initCarousel(element.parent());
			}
		}
	};
}]);
```




##### Issues

[double compilation]( https://docs.angularjs.org/guide/compiler#double-compilation-and-how-to-avoid-it )

- 文件命名问题

- 如果一个文件出错，那么会导致 module not found error.
- 每个浏览器对语法的严格程度不同
- 玄学改文件名解决依赖问题

#### controller

##### 关于inject

```js
angular.module('ngAppStrictDemo', [])
// BadController will fail to instantiate, due to relying on automatic function annotation,
// rather than an explicit annotation
.controller('BadController', function($scope) {
  $scope.a = 1;
  $scope.b = 2;
})
// Unlike BadController, GoodController1 and GoodController2 will not fail to be instantiated,
// due to using explicit annotations using the array style and $inject property, respectively.
.controller('GoodController1', ['$scope', function($scope) {
  $scope.a = 1;
  $scope.b = 2;
}])
```

##### 关于CSS样式

```js
div[ng-controller] {
    margin-bottom: 1em;
    -webkit-border-radius: 4px;
    border-radius: 4px;
    border: 1px solid;
    padding: .5em;
}
```

#### ngApp

The `ngApp` directive designates the **root element** of the application and is typically placed near the root element of the page - e.g. on the `` or `` tags. 

*  only one AngularJS application can be auto-bootstrapped per HTML document.  
*  AngularJS applications cannot be nested within each other. 
*  Do not use a directive that uses [transclusion](https://docs.angularjs.org/api/ng/service/$compile#transclusion) on the same element as `ngApp`. 
  *  Transclusion is the process of extracting a collection of DOM elements from one part of the DOM and copying them to another part of the DOM, while maintaining their connection to the original AngularJS scope from where they were taken. 

#### Provider

[refer]( https://docs.angularjs.org/api/auto/service/$provide#factory )

##### ControllerProvider

The [$controller service](https://docs.angularjs.org/api/ng/service/$controller) is used by AngularJS to create new controllers.

This **provider** allows controller registration via the [register](https://docs.angularjs.org/api/ng/provider/$controllerProvider#register) method.

`$controller` service is responsible for instantiating controllers.

It's just a simple call to [$injector](https://docs.angularjs.org/api/auto/service/$injector), but extracted into a service, so that one can override this service with [BC version](https://gist.github.com/1649788).

[Providers]( https://docs.angularjs.org/guide/providers#provider-recipe )

The Provider recipe is syntactically defined as a custom type that implements a `$get` method. This method is a factory function just like the one we use in the Factory recipe. In fact, if you define a Factory recipe, an empty Provider type with the `$get` method set to your factory function is automatically created under the hood. 

| Features / Recipe type           | Factory | Service | Value | Constant | Provider |
| :------------------------------- | :------ | :------ | :---- | :------- | :------- |
| can have dependencies            | yes     | yes     | no    | no       | yes      |
| uses type friendly injection     | no      | yes     | yes*  | yes*     | no       |
| object available in config phase | no      | no      | no    | yes      | yes**    |
| can create functions             | yes     | yes     | yes   | yes      | yes      |
| can create primitives            | yes     | no      | yes   | yes      | yes      |

#### angular.module

The `angular.module` is a global place for creating, registering and retrieving AngularJS modules. All modules (AngularJS core or 3rd party) that should be available to an application must be registered using this mechanism.

Passing one argument retrieves an existing [`angular.Module`](https://docs.angularjs.org/api/ng/type/angular.Module), whereas passing more than one argument creates a new [`angular.Module`](https://docs.angularjs.org/api/ng/type/angular.Module)

#### config

```js
myApp.config(["unicornLauncherProvider", function(unicornLauncherProvider) {
  unicornLauncherProvider.useTinfoilShielding(true);
}]);
```

Use this method to configure services by injecting their [`providers`](https://docs.angularjs.org/api/ng/type/angular.Module#provider), e.g. for adding routes to the [$routeProvider](https://docs.angularjs.org/api/ngRoute/provider/$routeProvider).

Note that you can only inject [`providers`](https://docs.angularjs.org/api/ng/type/angular.Module#provider) and [`constants`](https://docs.angularjs.org/api/ng/type/angular.Module#constant) into this function.

#### Naming Convention

module, controller, etc. 所有前缀都是小写！！！！

#### Questions

1. how to compile & link?

