### 头部组件

##### 涉及到的知识点   
> 指令部分    
> 指令属性的值预期是单个 JavaScript 表达式 (v-for 是例外情况)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。    
> `<p v-if="seen">现在你看到我了</p>`  
> `v-if 指令将根据表达式 seen 的值的真假来插入/移除 <p> 元素`  
   
#### 一些指令能够接收一个“参数”，在指令名称之后以冒号表示	
> 完整语法 v-bind:href="url"   缩写  :href="url"  
> 完整语法 v-on:click="doSomething"   缩写  @click="doSomething" 
> v-bind:class 可以传给 v-bind:class 一个对象，以动态地切换 class
> 可以在对象中传入更多属性来动态切换多个 class。此外，v-bind:class 
> 指令也可以与普通的 class 属性共存。
> 比如：`v-bind:class="{ active: isActive, 'text-danger': hasError }`

####  v-if vs v-show       
> v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
> v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
> 相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
> 一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

####  v-if 与 v-for 一起使用
>   v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级

#### 用 v-for 通过一个对象的属性来迭代
>  `<li v-for="value in object">`
>   ` {{ value }}`
>  `</li>`

#### 也可以提供第二个的参数为键名：
>  `<div v-for="(value, key) in object">`
>  `  {{ key }}: {{ value }}`
>  `</div>`

#### 第三个参数为索引：
>  `<div v-for="(value, key, index) in object">`
>  `  {{ index }}. {{ key }}: {{ value }}`
>  `</div>`





 
