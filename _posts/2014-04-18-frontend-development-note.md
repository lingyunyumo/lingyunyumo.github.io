---
layout: post
title: "前端开发学习笔记"
tags: 
  - AngularJS
  - Bootstrap
---

## 概要

前阵子巧遇AngularJS，玩了几天。

一开始很变扭，用jQuery的思维完全思路混乱，习惯了后————就如其宣称的————感觉不像是在写前端的程序。

虽然暂时用不着，不过记录下应该是不错的做法。

学的过程中写了个Demo。

整个Demo打包在此：[Demo](https://dl.dropboxusercontent.com/u/41623647/frontend_demo.rar)。随意找个Web服务器部署下就可查看，由于WebService部分没有打包进去，运行时有些地方会Error>_<.)

主要文件有：

* index.html - 由于是单页面的WebApp，这便是框架视图
* welcome.html - 欢迎内容子页
* login.html - 登录内容子页
* new.html - 新建内容子页面
* app.js - 包含应用逻辑的javascript脚本

用到的一些模块：

* angular-grid - angularJS下的表格模块
* ui-bootstrap-tpls-0.10.0 - 以angularJS风格来使用Bootstrap
* angular-translate - 实时的界面多语言模块

### 关键文件

index.html文件：

{% highlight html %}
<!DOCTYPE html>
<html ng-app="project">
<head>
  <meta http-equiv="content-language" content="zh-cn" />
  <meta http-equiv="content-type" content="text/html; charset=utf-8" />
  <meta name="author" content="http://taoxiaolei.cn" />
  <meta name="description" content="" />
  <meta name="keywords" content="" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0.0" >
  <title translate="TITLE">Anotherr Demo</title>
  <link rel="icon" type="image/png" href="img/favicon.png" />
  <link rel="stylesheet" href="static/bootstrap/css/bootstrap.min.css" type="text/css" />
  <link rel="stylesheet" href="static/angular-1.2.13/angular-grid.min.css" type="text/css" />
  <link rel="stylesheet" href="static/app.css" type="text/css" />
  
  <script src="static/jquery/jquery-1.10.2.min.js"></script>
  <script src="static/bootstrap/js/bootstrap.min.js"></script>
  <script src="static/angular-1.2.13/angular.min.js"></script>
  <script src="static/angular-1.2.13/angular-resource.min.js"></script>
  <script src="static/angular-1.2.13/angular-cookies.min.js"></script>
  <script src="static/angular-1.2.13/angular-route.min.js"></script>
  <script src="static/angular-1.2.13/angular-grid.min.js"></script>
  <script src="static/ui-bootstrap-tpls-0.10.0.min.js"></script>
  <script src="static/angular-translate.min.js"></script>
  <script src="static/loader-static-files.js"></script>
  <script src="static/app.js"></script> 
</head>
<body>

<!-- Fixed navbar -->
<div class="navbar navbar-inverse navbar-fixed-top">
  <div class="container">
  <div class="navbar-header">
    <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    </button>
    <a class="navbar-brand" href="#/">{{"BRAND"|translate}}：{{ user }}</a>
  </div>
  <div class="navbar-collapse collapse">
    <ul class="nav navbar-nav">
      <li ><a href="#/">{{"HOME"|translate}}</a></li>
      <li><a href="#/about">{{"ABOUT"|translate}}</a></li>
    </ul>
  </div>
  </div>
</div>
  
<div class="container">
<div ng-view></div>
</div>

<div class="text-center" style="background-color:Black;color:White;margin-top:20px;">
Another Demo. Copyright © 2014 Company All Rights Reserved.
</div>

</body>
</html>
{% endhighlight %}

welcome.html文件：

{% highlight html %}
<div>
  <h1>{{"welcome.HEADER"|translate}}</h1>
</div>

<div class="row">

<div class="col-md-6">
  <div class="panel panel-default">
    <div class="panel-heading">{{"welcome.FILE"|translate}}</div>
    <div class="panel-body">
      <a href="#/new" class="btn btn-success">{{"welcome.NEW"|translate}}</a>
      <a href="#/open" class="btn btn-success">{{"welcome.OPEN"|translate}}</a>
      <a href="#/save" class="btn btn-success">{{"welcome.SAVE"|translate}}</a>
      <a href="#/saveas" class="btn btn-success">{{"welcome.SAVEAS"|translate}}</a>
    </div>
  </div>
</div>

<div class="col-md-6">
  <div class="panel panel-default">
    <div class="panel-heading">
      <h3 class="panel-title">{{"welcome.SETTINGS"|translate}}</h3>
    </div>
    <div class="panel-body">
      <a href="#/language" class="btn btn-success">{{"welcome.LANGUAGE"|translate}}</a>
      <a href="#/units" class="btn btn-success">{{"welcome.UNITS"|translate}}</a>
    </div>
  </div>
</div>

<div class="col-md-6">
  <div class="panel panel-default">
    <div class="panel-heading">
      <h3 class="panel-title">{{"welcome.LANGUAGE"|translate}}</h3>
    </div>
    <div class="panel-body">
      <button class="btn btn-success" ng-click="setLang('en_US')">{{"en_US"|translate}}</button>
      <button class="btn btn-success" ng-click="setLang('zh_CN')">{{"zh_CN"|translate}}</button>
    </div>
  </div>
</div>

</div>
{% endhighlight %}

app.js文件：

{% highlight javascript %}
var app = angular.module('project', ['ngRoute', 'ngCookies', 'ngResource', 'ngGrid', 'ui.bootstrap', 'pascalprecht.translate'])

app.config(function ($routeProvider) {
    $routeProvider
    .when('/', {
        controller: 'WelcomeCtrl',
        templateUrl: 'welcome.html'
    })
    .when('/new', {
        controller: 'NewCtrl',
        templateUrl: 'new.html'
    })
    .when('/richpage', {
        controller: 'RichPageCtrl',
        templateUrl: 'richpage.html'
    })
    .when('/login', {
        controller: 'LoginCtrl',
        templateUrl: 'login.html'
    })
    .otherwise({
        redirectTo: '/'
    });
});

app.config(['$translateProvider', function ($translateProvider) {
    $translateProvider.useStaticFilesLoader({
        prefix: 'static/lang/',
        suffix: '.json'
    });

    // Tell the module what language to use by default
    $translateProvider.preferredLanguage('en_US');

} ]);

app.controller('LoginCtrl', function ($scope, $location, $cookies, $timeout) {
    $scope.login = function () {
        $cookies.user = $scope.user;
        $cookies.password = $scope.password;
        $location.path('/');
    };

    //$timeout(function() { $location.path('/'); });
});

app.controller('WelcomeCtrl', function ($scope, $location, $cookies, $timeout, $rootScope, $translate) {
    if (!($cookies.user)) {
        $location.path('/login');
    }
    $rootScope.user = $cookies.user;
    $scope.setLang = function (lang) {
        $translate.use(lang);
    }
    
});

app.controller('RichPageCtrl', function ($scope, $location, $cookies, $timeout, $http) {
    if (!($cookies.user)) {
        $location.path('/login');
    }
    $scope.calculate = function () {
        $http.get("static/forTable.json").success(function (data, status, headers, config) {
            console.log('http.get() success1.');
            $scope.results = [{ heatexchanger: 'D30-H-68', units: 1 },
                        { heatexchanger: 'D30-42', units: 1 },
                        { heatexchanger: 'D30-56', units: 1}];

        });
    };
});

app.controller('NewCtrl', function ($scope, $location, $timeout, $http) {
    $http.get("service/gui/new/bigclasses")
    .success(function (data, status, headers) {
        $scope.bigclasses = data;
    })
    .error(function (data, status, headers) {
        alert("error");
    });

    $scope.myChange1 = function (selectedValue1) {
        $http.get("service/gui/new/smallclasses", { params: { bigclassid: selectedValue1} })
        .success(function (data, status, headers) {
            $scope.smallclasses = data;
        })
        .error(function (data, status, headers) {
            alert("error");
        });
    };

    $scope.OK = function () {
        console.log('clicked.');
        //if ($scope.selectedValue1 == "0") {
            $location.path('/richpage');
        //}
    };

});
{% endhighlight %}