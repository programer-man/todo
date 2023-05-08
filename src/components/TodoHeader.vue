<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll"/>
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keydown.enter="add"
      v-model="newTest"
    />
  </header>
</template>

<script>
export default {
    // 可以得到 父组件里的 数据
    props: ['arr'],
    data(){
        return{
            newTest:'',
        }
    },
  methods: {
    add(){
        //判断输入框内是否有 任务名
        if(this.newTest === ''){
            return
        }
        // 创建一个新对象
        let obj = {
            id: this.arr.length === 0 ? 100:this.arr[this.arr.length-1].id + 1,
            name: this.newTest,
            isDone: false
        }
        // 触发父组件的 addTest 事件
        this.$emit('addTest', obj)
        // 将输入框清空
        this.newTest = ''
        // this.arr.push(obj)
    },
   
  },
  computed:{
    isAll:{
        set(checked){
            this.arr.forEach( obj => obj.isDone = checked)
        },
        get(){
            this.arr.every(obj => obj.isDone === true)
        }
    }
  }
};
</script>