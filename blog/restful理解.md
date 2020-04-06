# 路由名称

参考了[HTTP API Design Guide](https://github.com/interagent/http-api-design),此文有描述路由接口的设计
还有，我们在设计自己的接口规范的时候，


## 现状
现在的路由支持动态路径参数```/resources/:resource/actions/:action```,但是我从来没用过
```

```
### 版本
```
	"/api/v1/template/get":         {[]string{"GET"}, api.GetFromCacheById},   //APP模板请求
	"/api/v2/template/get":         {[]string{"GET"}, api.GetAppTemplateV2},   //APP模板请求
	"/api/v3/template/get":         {[]string{"GET"}, api.GetAppTemplateV3},   //APP模板请求V3，ios版本 <=105
	"/api/v4/template/get":         {[]string{"GET"}, api.GetAppTemplateV4},   //APP模板请求V4，ios版本 >105
	"/api/v5/template/get":         {[]string{"GET"}, api.GetAppTemplateV5},   //APP模板请求V5，android专用
	"/api/v6/template/get":         {[]string{"GET"}, api.GetAppTemplateV6},   //APP模板请求
```


## 资源
明确资源的层级关系


## 动作
为了直观，在末尾使用action


## 语法














## 参考
[HTTP API 设计强制规范](https://www.jianshu.com/p/36d55141277e)
https://segmentfault.com/a/1190000016655709

https://blog.csdn.net/guofeng93/article/details/93098736
