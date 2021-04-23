---
title: VUE基础：组件之间传值的几个方法
tags: [vuejs,javascript,nodejs]
id: '696'
categories:
  - - 计算机编程
abbrlink: c79feebc
date: 2019-07-07 14:26:03
---

一、属性传值，父传子

<template>     <!--   父组件 -->  
  <div style="margin-top: 100px">  
    <child-component v-bind:ddd="ddd">  
    </child-component>  
  </div>  
</template>  
<script>  
import demo1 from './demo1.vue'  
  
export default {  
  name: 'demo',  
  data: function () {  
    return {  
      ddd: '1111'  
    }  
  } }  
</script>

<template>    <!--   子组件 -->   
  <div>  
    <p @click="ccc">点击我</p>  
  </div>  
</template>  
  
<script>  
  export default {  
    name: 'demo1',  
    props: {  
      ddd: {  
        type: String  
      }  
    },  
    methods: {  
      ccc: function () {  
        console.log(this.ddd)   <!--   会打印该值 -->   
      }  
    }  
  }  
</script>

在多个子组件的关系当中，其中一个子组件有一个方法，在当前组件中，改变了从父组件传过来的值，那么只会影响当前组件的传值值，不会改变其他的组件和父组件的值

二、属性传对象或列表，父传子

 props: {         <!--   子组件   具体函数参考上面 -->   
      ddd: {  
        type:  Object  
      } 

在多个子组件中传对象或列表，如果一个子组件发生了改变，其他的组件也会发生改变

三、事件传值，子传父

<demo2 v-bind:ddd="ddd" v-on:zitofu="updatezitofu($event)"> </demo2>            <!--   父组件 --> 

methods: {        
  updatezitofu: function (event) {  
    console.log(event)      //打印子组件里面值 '子向父事件传值'   
  }  
},

<p @click="ccc">点击我</p>     <!--   子组件 -->  

methods: {  
  ccc: function () {  
    this.$emit('zitofu', '子向父事件传值')  
  }  
}

四：兄弟组件之间传值（事件传值）

它是在第三个子传父事件基础上，给父组件绑定一个属性传给兄弟组件，然后用props绑定

五：兄弟元素之间传值（$on和$emit）,新建一个etcjs.js并且vue实例化它

import Vue from 'vue'       //etc.js
export default new Vue()

兄弟组件A，内容如下

import etcjs from './etcjs.js'  
export default {  
  name: 'demo2',  
  methods: {  
    ccc: function () {  
      etcjs.$emit('myfun', this.shib)  
    }  
  }  
}

兄弟组件B，内容如下

import etcjs from './etcjs'  
export default {  
  name: 'demo1',  
  data: function () {  
    return {  
      shia: '文本1',  
    }  
  },  
  mounted: function () {  
    etcjs.$on('myfun', (message) => {  
      this.shia = message     //在这里用钩子函数将值绑定到当前组件  
    })  
  }  
}