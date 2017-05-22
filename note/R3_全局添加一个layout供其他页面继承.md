### 记得以前每次加上html文件，都要加上如下的信息

```
<!DOCTYPE html>
<html>
  <head>
  资源文件
  </head>
  <body>
  正文
  </body>
</html>
```

### 如果是<head>里头有些资源文件如js/css是需要复用的话，以前我的解决方法有：

- 创建一个html文件，把复用的塞进去，开启服务器的SSI，然后在<head>使用include的方式引入这个html。这种方法在include再次嵌套include，会导致某个服务器解析不正常，比如wamp

- 要不就是ajax去请求这个html文件，然后append到某个元素上

以上这些方法都有各自的缺点，偶尔一次看到webpack有includde html这种东西，可以在.VUE使用import来引入一个html文件。
有点扯远了，回到正题，在单页面只有一个html文件作为如果，其他都继承上面的代码，但是如果是多页面，不可能每次加一个html文件，然后去复制上面的代码到新的html吧，如果加了20个html,如果公用的东西需要修改，那就要改20次，苦逼啊，所以我希望页面都继承上面代码的内容，同时上面代码针对一些页面增加一些可覆盖性或者可增加的代码接口给新的html来修改。这功能至少我现在在webpack或者gulp有这方面的实现，至少服务器语言php，nodejs这些是可以的，后来看了nuxt.js，可以实现这样的效果。

- 网站根目录创建app.html

```
<!DOCTYPE html>
<html {{ HTML_ATTRS }}>
  <head>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    {{ APP }}
  </body>
</html>
```

比如在pages下面创建center/index.vue

```
<template>
  <section class="container">
    收藏
  </section>
</template>
<script>
</script>
<style scoped>
</style>
```
那么生成后的html是包含上面app.html的模板的

```
<!DOCTYPE html>
<html {{ HTML_ATTRS }}>
  <head>
    <script src="/libs/flexible.js"></script>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    {{ APP }}
  </body>
</html>
```
app.html这个东西修改后要重新npm run dev一次，不然没有效果，大概没把它放到监听范围上吧
如果想针对head标签定义东西的话，可以在nuxt.config.js继进行修改

```
head: {
  title: 'starter',
  meta: [
    { charset: 'utf-8' },
    { name: 'viewport', content: 'width=device-width, initial-scale=1' },
    { hid: 'description', name: 'description', content: 'Nuxt.js project' }
  ],
  link: [
    { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
  ]
}
```




