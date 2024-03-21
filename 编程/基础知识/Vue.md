---
日期: 2024-03-20
tags:
  - 快速开始
---
# 新建Vue项目


# 路由方法（路由跳转）
**创建路由**：
1. 在main.js中引入全局路由
```js
import router from './router'
createApp(App).use(router)
```
1. router/index.js 路径下
```js
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
- a跳转 `<a href="selfManage">`
- `<router-link>`路由:当点击About会跳转到/about
	```html
	<router-link to="/about">About</router-link>
	```
	- [[前端开发经验#路由的时候传递参数|动态传参路由]]：
	```js
	{ path: '/user/:id',name: 'user', component: User }
	```
```html
<router-link :to="{ name: 'user', params: { id: userId }}">User Profile</router-link>
```
- `this.$router.push('/purchase/${productId}');` 路由
- setup发送路由： ^10ad03
```js
	import { useRouter } from 'vue-router';
	const router=useRouter();
	router.push(`/servicesBuy/${id}`);
```

^20a2b6


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

# ref,reactive数组的操作
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


# 前端展示后端发来的html
## 利用 v-html
**缺点**：如果包含js代码则不能执行，是静态的
```vue
<template>
  <div>
    <!-- 使用 v-html 渲染 HTML 内容 -->
    <div v-html="htmlContent"></div>
  </div>
</template>
<script>  
export default defineComponent({  
setup() {  
//用于存储后端返回的表单内容  
const formContent =ref('11');  
const buyMethod = () => {  
	formContent.value="<h1>Hello, World!</h1>";  
	}  
return {formContent};  
},  
});  
</script>
```
## 利用document.write()
**缺点**：它会直接写入到文档流中，可能会覆盖当前页面的内容，可能会清除当前页面的内容，而且在加载期间页面会出现空白。但会执行其中的js代码
**==使用场景**： 支付宝支付，后端返回给前端的页面==
```js
const responseHtml = resp.data.content;
document.open();
document.write(responseHtml);
document.close();
```