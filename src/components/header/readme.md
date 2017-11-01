### 头部组件

##### 涉及到的知识点   
> 指令部分    
- v-if     
> `<p v-if="seen">现在你看到我了</p>`  
> `v-if 指令将根据表达式 seen 的值的真假来插入/移除 <p> 元素`  
   
#### 一些指令能够接收一个“参数”，在指令名称之后以冒号表示	
> 完整语法 v-bind:href="url"   缩写  :href="url"  
> 完整语法 v-on:click="doSomething"   缩写  @click="doSomething" 
> v-bind:class 可以传给 v-bind:class 一个对象，以动态地切换 class
> 可以在对象中传入更多属性来动态切换多个 class。此外，v-bind:class 
> 指令也可以与普通的 class 属性共存。
> 比如：`v-bind:class="{ active: isActive, 'text-danger': hasError }`




 
