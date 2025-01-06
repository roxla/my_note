# Vue3

> 

## 组件化

> 

### 为组件的 props 标注类型

> **使用`<script setup>`**
>
> 

#### props 类型说明

> **props 的 type 的类型只支持如下几种**
>
> - `String`
> - `Number`
> - `Boolean`
> - `Array`
> - `Object`
> - `Date`
> - `Function`
> - `Symbol`
>
> 使用`vue3.0` 对 `props` 进行复杂类型验证的时候，可以直接用 `PropType` 进行强制转换
>
> ```typescript
> const props = {
>     timelineApi: { type: Function as PropType<PromiseFn> },
>     mode: { type: String as PropType<'' | 'alternate' | 'left' | 'right'> },
>     pending: { type: [Boolean, String], default: false },
>     pendingDot: { type: String },
>     reverse: { type: Boolean, default: false },
>     titleStyle: { type: Object as PropType<CSSProperties>, default: () => ({}) },
>     descStyle: { type: Object as PropType<CSSProperties>, default: () => ({}) },
> };
> ```
>
> `PropType` 使`props`获得了更准确的类型推论，让我们在使用属性的时候获取更丰富的类型提示

## 组合式 API

> 

### setup

> 新的option, 所有的组合API函数都在此使用, 只在初始化时执行一次
>
> 函数如果返回对象, 对象中的属性或方法, 模板中可以直接使用
>
> **注意**
>
> - 如果在父组件的 `setup` 中存在异步逻辑（例如 `await` 请求数据），那么 Vue 会先执行子组件的渲染，等待父组件的异步逻辑完成后再继续父组件的更新

### Ref全家桶

> **ref、isRef、shallowRef、triggerRef、customRef**

#### ref

> **概述**
>
> 接受一个内部值并返回一个响应式且可变的 ref 对象。ref 对象仅有一个 `.value` property，指向该内部值
>
> **语法**
>
> ```typescript
> const xxx = ref(initValue)
> ```
>
> - 创建一个包含响应式数据的引用(reference)对象
> - js中操作数据： xxx.value
> - 模板中操作数据：不需要.value
>
> *一般用来定义一个基本类型的响应式数据*
>
> **案例**
>
> 我们这样操作是无法改变message 的值 应为message 不是响应式的无法被vue 跟踪要改成ref
>
> ```typescript
> <template>
>   <div>
>     <button @click="changeMsg">change</button>
>     <div>{{ message }}</div>
>   </div>
> </template>
> <script setup lang="ts">
> let message: string = "我是message"
> 
> const changeMsg = () => {
>    message = "change msg"
> }
> </script>
> ```
>
> *改为 ref*
>
> Ref TS对应的接口
>
> ```typescript
> // T 为包装的值的类型
> interface Ref<T> {
>     value: T
> }
> ```
>
> `注意被 ref 包装之后需要.value 来进行赋值`
>
> 方式一
>
> ```typescript
> <template>
>   <div>
>     <button @click="changeMsg">change</button>
>     <div>{{ message }}</div>
>   </div>
> </template>
> <script setup lang="ts">
> import {ref, Ref} from 'vue'
> let message:Ref<string> = ref("我是message")
> 
> const changeMsg = () => {
>    message.value = "change msg"
> }
> </script>
> ```
>
> 方式二
>
> ```typescript
> <template>
>   <div>
>     <button @click="changeMsg">change</button>
>     <div>{{ message }}</div>
>   </div>
> </template>
> <script setup lang="ts">
> import { ref } from 'vue'
> let message = ref<string | number>("我是message")
> 
> const changeMsg = () => {
>   message.value = "change msg"
> }
> </script>
> ```

##### ref源码

> **ref方法**
>
> ```typescript
> export function ref(value?: unknown) {
>  return createRef(value, false)
> }
> ```
>
> `ref`方法内部调用`createRef`方法来构建
>
> **createRef**
>
> ```typescript
> function createRef(rawValue: unknown, shallow: boolean) {
>  if (isRef(rawValue)) {
>      return rawValue;
>  }
>  return new RefImpl(rawValue, shallow);
> }
> ```
>
> 在该方法中，先判断传进来的值`rawValue`是否为`ref对象`。是的话直接返回该对象，不是的话使用`new RefImpl`来构建对象
>
> **RefImpl类**
>
> ```typescript
> class RefImpl<T> {
>    private _value: T
>    private _rawValue:T
> 
>    public dep?: Dep = undefined
>    public readonly __v_isRef = true
> 
>    constructor(value: T, public readonly __v_isShallow: boolean) {
>      this._rawValue = __v_isShallow ? value : toRaw(value)
>      this._value = __v_isShallow ? value : toReactive(value)
>    }
> 
>    get value() {
>      trackRefValue(this)
>      return this._value
>    }
> 
>    set value(newVal) {
>      newVal = this.__v_isShallow ? newVal: toRaw(newVal)
>      if (hasChanged(toRaw(newVal), this._rawValue)) {
>        this._rawValue = newVal
>        this._value = this._shallow ? newVal : convert(newVal)
>        trigger(toRaw(this), TriggerOpTypes.SET, 'value', newVal)
>      }
>    }
> }
> ```
>
> 可以看见`RefImpl class`传递了一个泛型类型T，做了如下操作
>
> - 申明一个私有属性` _value`内容为泛型T，申明了一个公开只读属性`__v_isRef`值为 true
> - 有一个构造函数`constructor`，用于构造对象。构造函数接受两个参数：
>   - 第一个参数 `_rawValue`，要求是`T`类型
>   - 第二个参数 `__v_isShallow`，要求是`boolean`类型
> - 提供了两个方法，get value(){} 和 set value(){}，分别对应私有属性的读写操作，用于供外界操作`value`
>
> 当通过它构建对象时，会给对象的 `_value` 属性赋值为 `_rawValue` 或者 `toReactive(value)`
>
> **toReactive**
>
> ```typescript
> export const toReactive = <T extends unknown>(value: T): T => isObject(value) ? reactive(value) : value
> ```
>
> 最终Vue会根据传入的数据是不是对象isObject(val)，如果是对象调用的是reactive方法，否则返回原始数据

#### isRef

> **作用**
>
> 判断是不是一个ref对象
>
> **示例**
>
> ```typescript
> import { ref, Ref,isRef } from 'vue'
> let message: Ref<string | number> = ref("我是message")
> let notRef:number = 123
> const changeMsg = () => {
>    message.value = "change msg"
>    console.log(isRef(message)); //true
>    console.log(isRef(notRef)); //false
> }
> ```

#### unref

> **作用**
>
> 如果参数是一个 ref 则返回它的 value，否则返回参数本身
>
> *unref()：是 val = isRef(val) ? val.value : val 的语法糖*
>
> **示例**
>
> ```typescript
> const valueRef = ref('');
> const value = unref(valueRef);
> if (!value) {
>     console.warning('请输入要拷贝的内容！');
>     return;
> }
> ```

#### shallowRef

> **作用**
>
> 创建一个跟踪自身 `.value` 变化的 ref，但不会使其值也变成响应式的
>
> **示例**
>
> 修改其属性是非响应式的这样是不会改变的
>
> ```typescript
> <template>
> <div>
>  <button @click="changeMsg">change</button>
>  <div>{{ message }}</div>
> </div>
> </template>
> <script setup lang="ts">
> import { Ref, shallowRef } from 'vue'
> type Obj = {
> name: string
> }
> // 只监控 message 自身的 value 的修改
> let message: Ref<Obj> = shallowRef({
> name: "小满"
> })
> // value 内的属性的值的更改不会被跟踪
> const changeMsg = () => {
> message.value.name = '大满'
> }
> </script>
> 
> ```
>
> 这样是可以被监听到的修改value
>
> ```typescript
> import { Ref, shallowRef } from 'vue'
> type Obj = {
>  name: string
> }
> let message: Ref<Obj> = shallowRef({
>  name: "小满"
> })
> // 修改 value 的值，会被监听
> const changeMsg = () => {
>  message.value = { name: "大满" }
> }
> ```

#### triggerRef

> **作用**
>
> 强制更新页面DOM
>
> **示例**
>
> 这样也是可以改变值的
>
> ```typescript
> <template>
>  <div>
>      <button @click="changeMsg">change</button>
>      <div>{{ message }}</div>
>  </div>
> </template>
> <script setup lang="ts">
>  import { Ref, shallowRef,triggerRef } from 'vue'
>  type Obj = {
>      name: string
>  }
>  let message: Ref<Obj> = shallowRef({
>      name: "小满"
>  })
> 
>  const changeMsg = () => {
>      message.value.name = '大满'
>      triggerRef(message)
>  }
> </script> 
> ```

#### customRef

> **作用**
>
> 自定义ref
>
> **示例**
>
> customRef 是个工厂函数要求我们返回一个对象 并且实现 get 和 set
>
> ```typescript
> <script setup lang="ts">
> import { Ref, shallowRef, triggerRef, customRef } from 'vue'
> 
> function Myref<T>(value: T) {
> return customRef((track, trigger) => {
>  return {
>    get() {
>      track()
>      return value
>    },
>    set(newVal: T) {
>      console.log('set');
>      value = newVal
>      trigger()
>    }
>  }
> })
> }
> 
> let message = Myref('小满')
> const changeMsg = () => {
> message.value = '大满'
> // triggerRef(message)
> }
> </script> 
> ```
>
> - `customRef`的两个参数：
>   - track：追踪当前数据
>   - trigger：触发响应，即更新界面
> - 通过`customRef`返回的`ref`对象，和正常`ref`对象一样,通过`x.value`修改或读取值
>
> **类型声明**
>
> ```typescript
> function customRef<T>(factory: CustomRefFactory<T>): Ref<T>
> type CustomRefFactory<T> = (track: () => void, trigger: () => void) => {
>     get: () => T
>     set: (value: T) => void
> }
> ```
>
> **自定义防抖的ref**
>
> ```typescript
> function useDebouncedRef(value, delay = 200) {
>   let timeout
>   return customRef((track, trigger) => {
>     return {
>       get() {
>         track()
>         return value
>       },
>       set(newValue) {
>         clearTimeout(timeout)
>         timeout = setTimeout(() => {
>           value = newValue
>           trigger()
>         }, delay)
>       }
>     }
>   })
> }
> 
> export default {
>   setup() {
>     return {
>       text: useDebouncedRef('hello')
>     }
>   }
> }
> 
> <input v-model="text" />
> ```

### to系列全家桶

#### toRef

> 

#### toRefs

> 

#### toRaw

> 

## Hooks

> 

## 声明文件

> **概述**
>
> **声明文件就是给js代码补充类型标注**。这样在ts编译环境下就不会提示js文件"缺少类型"
>
> 声明变量使用关键字`declare`来表示声明其后面的**全局**变量的类型, 比如：
>
> ```typescript
> // packages/global.d.ts
> declare var __DEV__: boolean
> declare var __TEST__: boolean
> declare var __BROWSER__: boolean
> declare var __RUNTIME_COMPILE__: boolean
> declare var __COMMIT__: string
> declare var __VERSION__: string
> ```
>
> 看过vue3源码的同学一定知道这些是vue中的变量, 上面代码表示`__DEV__`等变量是全局, 并且标注了他们的类型. 这样无论在项目中的哪个ts文件中使用`__DEV__`, 变量ts编译器都会知道他是`boolean`类型.

### TS函数的重载

> **全局方法的重载**
>
> ```typescript
> // 函数重载声明
> function message(options: object): void;
> function message(text: string, onClose?: Function): void;
> function message(text: string, mode: string, duration?: number): void;
> function message(text: string, duration?: number, onClose?: Function): void;
> 
> // 函数实现
> function message(
>     param1: string | object,
>     param2?: number | Function | string,
>     param3?: Function | number
> ) {...}
>     
> // 函数调用
> message(...);
> ```
>
> 111
>
> **对象内的方法的重载**
>
> ```typescript
> // 函数重载声明
> interface ShowMessage {
>     (options: object): void;
>     (text: string, onClose?: Function): void;
>     (text: string, mode: string, duration?: number): void;
>     (text: string, duration?: number, onClose?: Function): void;
> }
> interface Utils {
>     showMessage: ShowMessage;
> }
> 
> // 函数实现
> const utils: Utils = {
>     showMessage(
>         param1: string | object,
>         param2?: number | Function | string,
>         param3?: Function | number
>     ) {...},
> };
> 
> // 函数调用
> utils.showMessage(...);
> ```
>
> 111

## Vue Route

> 

## Vite

### vite打包库

> 