---
日期: 2024-03-20
tags:
  - 快速开始
aliases:
  - 前端开发
---
环境准备：Node.js[Node.js下载安装及环境配置教程](https://blog.csdn.net/WHF__/article/details/129362462)
查看版本：`node -v` `npm -v`

# 新建Vue项目
**前置**：安装VueCli脚手架`npm install -g @vue/cli` 
**创建**：`vue create web`
选择设置:
	1. (手动配配置) `Manually select features` ->
	2. (多选配置) `Babel` `Router` `Vuex` `Linter/Formatter(可选代码规范)`->
	3. (选择版本) `3.x` ->
	4. (历史模式url地址开启用`/`分割 不开启`#`) `y`->
	5. (Linter/Formatter(可选代码规范)) `EsLint with error prevention only` ->
	6. (规范检查时机) `Lint on save` ->
	7. (规范保存位置) `In package.json` ->
	8. (是否保存预算) `Yes` or `NO` ->
	9. (项目名) `输入项目名` 
**运行**：npm run serve
# axios使用
**前置**：`npm install axios`
**使用**：
1. `import axios from 'axios'`
2. axios.post(`路径`,` {参数}或ref` ,`添加消息头(可选)`) .then(resp=>{回调}).catch(error => {错误回调})
3. axios拦截器：[[封装工具类#Axios拦截器]]

# 路由
**创建路由**：
1. 在main.js中引入全局路由
```js
import router from './router'
createApp(App).use(router)
```
1. router/index.js 路径下
```js fold:设置路由路径
{  
	path: '/selfManage/:param',  
	component: () => import('../views/Manage/selfManage.vue'),  
	name: 'selfManage',
	meta: {  
		loginNeed: true  
	},  
	children: [
	{  
		path: 'myMessage',  
		component: () => import('../views/Manage/content/myMessage.vue'),  
	}, {  
		path: 'changeAvatar',  
		component: () => import('../views/Manage/content/changeAvatar.vue')  
	}  
	]
},
```

> [!Tip]- 参数
> `path` 路由和页面访问路径 `:param` 代表可传入参数
> `component` vue组件位置
> `meta` 定义参数，常用于路由判断是否需要登入
> `children[]` 子路由，子路由路径等于 /selfManage/myMessage

**路由跳转**：
- a跳转路由: `<a href="selfManage">`
- [[Vue概念#<router-view > 组件|<router-link>]]路由: 当点击About会跳转到/about
```html fold:代码示例
<router-link to="/about">About</router-link>
------携带参数的动态路由
{ path: '/user/:id',name: 'user', component: User }

<router-link :to="{ name: 'user', params: { id: userId }}">User Profile</router-link>
```
- 方法中路由
	- methods:{}中： `this.$router.push('/purchase/${productId}');` 
	- setup()发送路由: [[前端开发经验#<router-view >的时候传递参数(前端路由跳转传参)|传递参数和接受参数]]
```js
	import { useRouter } from 'vue-router';
	const router=useRouter();
	router.push(`/servicesBuy/${id}`);
```
^20a2b6

**路由拦截器**：[[封装工具类#路由拦截器]]


# 添加监听器
 添加监听器位置：一般在`onMounted` 或`mounted()` 中添加监听器
 ```js
onMounted(() => {  
	window.addEventListener('resize', handleResize);  
});
 ```
 监听器销毁：在`beforeUnmount()` 或 `onUnmounted()` 中删除监听器
```js
onUnmounted(() => {  
	window.removeEventListener('resize', handleResize);  
});
```

> [!Tip]- 监听器分类
> **resize** :监听窗口大小变化
> **scroll**: 监听滚动条变化

# ref,reactive响应式数组的操作
**ref数组**
	定义：`const array=ref([])` 
*添加：*
>例如array=\[1,2,3\]，newArray=\[4,5,6\]
>1. ==array.value.concat(newArray)== 结果：\[1,2,3,\[4,5,6\]\]
>2. ==array.value=\[...array.value, ...newArray\]== 结果：\[1,2,3,4,5,6\] 原因[[Vue概念#...的作用|...的作用]],直接赋值改变结果
>3. `array.value.push(newProducts)`和`array.value.push(...newProducts)`
>==注意：push是在之后添加 ，第二种是直接赋值覆盖==

*删除*：
1. 使用 `splice(index, count)` 删除,从索引为 index 的位置开始，删除 count 个元素
2. `pop()`：删除并返回数组的==最后一个元素==。 ^b3c853
3.  `shift()`：删除并返回数组的==第一个元素==。
*包含：*
1. `includes(数组名)`：判断是否包含数组，包含返回true,不包含返回false

**给数组中的{ }添加字段**
>


# 生产环境配置
1. 根目录下创建`.env."你的环境名"` 如`.env.dev`或`.env.prod`
2. 文件内设置: `NODE_ENV` 是定义环境名，`VUE_APP_`固定前缀
```
NODE_ENV=dev  
VUE_APP_POKENIAO=http://localhost:8000  
VUE_APP_NGINX=http://139.9.219.48:8080  
VUE_APP_IMAGE_SAVE=http://139.9.219.48:8083
```
3. 启用不同环境：package.json中设置`--mode 环境`
```
"scripts": {
	"serve": "vue-cli-service serve --mode dev",
	"build": "vue-cli-service build",
	"lint": "vue-cli-service lint"
}
```
4. 读取：在main.js入口文件中 通过`process.env.`
```
console.log("环境", process.env.NODE_ENV);  
console.log("服务器", process.env.VUE_APP_POKENIAO);  
console.log("图片nginx地址",process.env.VUE_APP_NGINX)  
console.log("保存图片java后端",process.env.VUE_APP_IMAGE_SAVE)
```