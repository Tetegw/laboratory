<template>
  <div>
    <div>
      <input type="text" v-model="myValue" v-focus="isFocus">
      <input type="button" value="切换聚焦" @click="isFocus = !isFocus">
    </div>
    <div>
      <input type="text" v-myShow="{'text': 'vue'}">
      <span>{{text}}</span>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      myValue: '',
      text: '',
      isFocus: true
    }
  },
  directives: {
    // 自定义指令对象
    focus: {
      // 钩子函数
      inserted (el) {
        el.focus()
      },
      componentUpdated (el, binding, vNode, oldvNode) {
        console.log('object')
        if (binding.value) {
          el.focus()
        }
      }
    },
    myShow: {
      inserted (el, binding, vNode, oldvNode) {
        console.log(binding.value.text)
        // this.text = binding.value.text   this是undefined
      }
    }
  }
}
/* bind：只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作。
inserted：被绑定元素插入父节点时调用 (父节点存在即可调用，不必存在于 document 中)。
update：所在组件的 VNode 更新时调用，但是可能发生在其孩子的 VNode 更新之前。指令的值可能发生了改变也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
componentUpdated：所在组件的 VNode 及其孩子的 VNode 全部更新时调用。
unbind：只调用一次，指令与元素解绑时调用。 */
</script>

<style>

</style>
