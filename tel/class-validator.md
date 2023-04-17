#node #done 

是一个用于验证javascript对象的库，可以用来验证前端和后端的对象，例如html表单的restful api请求。可以将验证规则用于装饰器附加到类的属性上。这些规则包括@isString,@isBoolean等等，可以使用修饰器组合规则，例如@isOptional和@min等等

需要注意的是class-validator依赖es6的装饰器特征，使用前，需要确保正确实配置了装饰器转换器。

如果是动态判断某一个值是否是必填或者需要校验可以使用@valiatorIf((object)[⇒object.xxx](http://xn--object-9z2c.xxx))来判断