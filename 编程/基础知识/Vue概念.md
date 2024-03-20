---
日期: 2024-03-19
tags:
  - 基本概念
---

# setup和methods
1. setup中定义的是==响应式数据、方法==,需要return出去。而methods不需要
>`setup`函数中直接修改`_servicesType`的值，那么在模板中使用该值的地方将会自动更新。
>
2. setup ==没有访问组件实例的上下文==`this` ,要用只能手动传入。methods则不需要
>如：setup(props, =={ emit }==) {const sendEvent = () => { ==emit('custom-event', '传递的数据');== }; return { sendEvent }; }
>而：methods: { sendEvent() { ==this.$emit('custom-event', '传递的数据');== } }
 ^4da24e
3. setup的参数
>setup(props,context)
>1. `props`：这是一个==包含了组件接收的所有属性的对象==。在 Vue 3 中，props 是通过 `props` 选项定义的，可以是响应式的或非响应式的。在 `setup` 函数中，您可以直接使用 `props` 对象来访问组件的属性。
>2. `context`：这是一个包含了一些重要的 ==Vue 实例属性和方法的对象==，通常是一个上下文对象。在 Vue 3 中，`context` 包含了以下属性和方法：
>
>- `attrs`：一个对象，包含了未在 props 中声明的父组件传递的属性。这对于编写高阶组件非常有用。
>- `slots`：一个函数，用于访问组件的插槽内容。
>- `emit`：一个函数，用于触发事件。通过调用 `emit` 方法，可以向父组件发送自定义事件。

# 解构赋值
解构赋值是一种在 JavaScript 中从数组或对象中提取数据并赋值给变量的方法。这种方式可以使代码更加简洁和易读。
如
```js
setup(props, context) { const emit = context.emit; }
```
等于
```js
setup(props, { emit }) { // 在这里直接使用 emit 方法 }
```
相当于将 `context` 对象中的 `emit` 属性解构出来并赋值给名为 `emit` 的变量，省去了中间变量的声明和赋值过程，使代码更加简洁易读。
# ...的作用
这是 JavaScript 中的扩展运算符，使用 `...` 运算符==可以将**数组**或**类数组对象**展开为一系列元素==
>举个例子，假设 `products.value` 是 `[1, 2, 3]`，`newProducts` 是 `[4, 5, 6]`。如果我们直接使用 `products.value.concat(newProducts)`，得到的结果将是 `[1, 2, 3, [4, 5, 6]]`，这是一个嵌套的数组。但是，如果我们使用 `[...products.value, ...newProducts]`，得到的结果将是 `[1, 2, 3, 4, 5, 6]`，这是一个扁平的数组，其中包含了所有的元素。
>因此，使用 `...` 运算符可以帮助我们更方便地合并数组，并确保得到的结果是一个扁平的数组。