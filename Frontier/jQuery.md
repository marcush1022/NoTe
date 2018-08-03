# DOM, document object model
`Programming interface of documents like [XML or HTML], and defined a method for program to access it and change its struct`;

`API(web或xml页面) = DOM + JS`;

# (function($){...})(jQuery), (function(arg){})(param), (function(){}){}, $(document).ready(function(){...})
`auto functions , and they are [variadic functions]`, function($){...}, function(arg){}, function(){}参数分别为$, arg, 无参;

# (function($){...})(jQuery)
用来定义一些需要预先定义的函数, 用于形成闭包, 使(function($){...})(jQuery)中`定义的方法和变量只能在此范围内使用`;

#function($){...}(jQuery), $(function(){})
`DOM加载完执行 (DOCUMENT IS READY)`
$(function($){...}), jQuery(function($){...}), $(document).ready(function(){...}), 作用一样, `在DOM加载之后执行`；

# $.fn.extend(obj) 和 $.extend(obj)
$.xxx = function(option){} 用于为jQuery类添加一个method xxx, $.extend(obj)为jQuery提供多个methods, `使用jQuery可以直接调用该method, 添加到jQuery的methods为global function`;

# add multiple methods to jQuery;
$.extend({
    add:function(a, b) {return a + b}
    multi:function(a, b) {return a * b}
});

$.add(3, 4); // 7;
$.multi(3, 5); // 15;

# combine varibales of jQuery;
var res = $.extend({}, {a:1, b:2}, {a:3, c:4}) // res = {a:3, b:2, c:4};

# $.fn.xxx 和 $.fn.extend
$.fn.xxx used for add `single method to jQuery`, and $.fn.extend used for `add multiple methods to jQuery`;
Added methods considered as `member functions` of jQuery, only `instance of jQuery` can use these functions;

# jQuery(function(){...}) == $(function(){...}) == $(document).ready(function(){...})
These three function has the same effect, will be `excuted when document is ready(fully loaded)`;


