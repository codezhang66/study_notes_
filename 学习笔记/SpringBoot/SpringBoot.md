# SpringBoot

## 1、

118

![image-20210406141411583](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210406141411583.png)

![image-20210406172941953](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210406172941953.png)







## springboot错误页面的原理

如果系统出现错误会由**ErrorPageCustomizer**转到error请求，再由**BasicErrorController**处理，处理有两种方式，一种响应式页面html处理，另一种是json字符串形式。

```java
//**ErrorPageCustomize
@Bean
public ErrorPageCustomizer errorPageCustomizer(DispatcherServletPath dispatcherServletPath) {
    return new ErrorPageCustomizer(this.serverProperties, dispatcherServletPath);
}

//**BasicErrorController**
@RequestMapping(produces = MediaType.TEXT_HTML_VALUE)
public ModelAndView errorHtml(HttpServletRequest request, HttpServletResponse response) {
    HttpStatus status = getStatus(request);
    Map<String, Object> model = Collections
        .unmodifiableMap(getErrorAttributes(request, getErrorAttributeOptions(request, MediaType.TEXT_HTML)));
    response.setStatus(status.value());
    
    //由该方法确定要去哪个页面（包含页面地址和页面内容）
    ModelAndView modelAndView = resolveErrorView(request, response, status, model);
    return (modelAndView != null) ? modelAndView : new ModelAndView("error", model);
}

@RequestMapping
public ResponseEntity<Map<String, Object>> error(HttpServletRequest request) {
    HttpStatus status = getStatus(request);
    if (status == HttpStatus.NO_CONTENT) {
        return new ResponseEntity<>(status);
    }
    Map<String, Object> body = getErrorAttributes(request, getErrorAttributeOptions(request, MediaType.ALL));
    return new ResponseEntity<>(body, status);
}


```

## 3、自动配置原理：

**1、springboot启动的时候会给我们加载大量的自动配置类。**

**2、在看我需要的功能springboot有没有默认写好的自动配置类。**

**3、在看看自动配置类中配置了哪些组件？（是否有我们需要的组件，如果有，就不不要我们配置了）**

**4、springboot的自动配置类和properties类绑定，给自动配置类中添加组建的时候，会从properties中获取某些属性，我们可以在properties中指定属性的值。**



**原理（*）：**

- spring boot加载所有的自动配置类
- 每个自动配置按条件生效，每个自动配置类都绑定一个properties文件，配置类中属性值从properties中取
- 生效的配置类会给容器中添加很多组件
- 只要容器中有这些组件，就相当于有这些功能。
- 定制化配置
  - 用户直接用自己的@Bean给容器中替换底层的组件。
  - 直接修改配置文件中的属性值。

## 4、拦截器原理：

![image-20210720134144512](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210720134144512.png)

![image-20210720134107487](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210720134107487.png)