ExecJS
======

ExecJS可以运行在Ruby JavaScript代码。它会自动选择
现有的最佳运行时间来评估你的JavaScript程序，然后
结果返回给你作为一个Ruby对象.

ExecJS支持这些运行时间:

* [therubyracer](https://github.com/cowboyd/therubyracer) - Google V8
  嵌入的Ruby
* [therubyrhino](https://github.com/cowboyd/therubyrhino) - Mozilla的Rhino嵌入的JRuby
* [Duktape.rb](https://github.com/judofyr/duktape.rb) - Duktape JavaScript解释器
* [Node.js](http://nodejs.org/)
* Apple JavaScriptCore - Included with Mac OS X
* [Microsoft Windows Script Host](http://msdn.microsoft.com/en-us/library/9bbdkx3k.aspx) (JScript)
* [Google V8](http://code.google.com/p/v8/)
* [mini_racer](https://github.com/discourse/mini_racer) - Google V8
  嵌入的Ruby

简单例子:

``` ruby
require "execjs"
ExecJS.eval "'red yellow blue'.split(' ')"
# => ["red", "yellow", "blue"]
```

较长的例子，演示了如何调用编译器的CoffeeScript:

``` ruby
require "execjs"
require "open-uri"
source = open("http://coffeescript.org/extras/coffee-script.js").read

context = ExecJS.compile(source)
context.call("CoffeeScript.compile", "square = (x) -> x * x", bare: true)
# => "var square;\nsquare = function(x) {\n  return x * x;\n};"
```

# 安装

```
$ gem install execjs
```

# FAQ

**为什么我不能使用CommonJS `require()` 里面ExecJS?**

ExecJS提供了一个最小公分母接口的JavaScript运行。
使用ExecJS时，它并不重要的JavaScript解释你的代码运行
。如果您要访问的节点API，你应该检查像另一个库
[commonjs.rb](https://github.com/cowboyd/commonjs.rb) 旨在提供一个
一致的界面.

**为什么我不能用 `setTimeout`?**

出于类似的原因为模块，并不是所有的运行时间保证一个完整的JavaScript
事件循环。 所以 `setTimeout`, `setInterval` 和其他定时器没有定义.

**为什么我不能用ES5功能?**

如Node一些运行时将实施许多最新的ES5功能。 然而
旧的股票运行时就像JSC在OSX和JScript的Windows上可能不会。 你应该
只有指望ES3的功能是可用的。不想功能检查这些API
具体运行时间，而不是硬编码的支持.

**ExecJS可用于沙箱脚本?**

无，ExecJS不应被用于任何与安全有关的沙盒。由于运行时间
自动检测，每个运行时都有不同的沙箱属性。
你不应该使用'ExecJS.eval`任何投入，你会感到不舒服的Ruby
`eval()`ing.

## 特约ExecJS

ExecJS is work of hundreds of contributors. You're encouraged to submit pull requests, propose
features and discuss issues.

See [CONTRIBUTING](CONTRIBUTING.md).

## License
ExecJS is released under the [MIT License](MIT-LICENSE).
