<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li  v-for="(obj, index) in list" :key="obj.id" :class="{completed:obj.isDone}" >
      <div class="view">
        <input class="toggle" type="checkbox" v-model="obj.isDone"/>
        <label>{{obj.name}}</label>
        <button class="destroy" @click="del(index)"></button>
      </div>
    </li>
  </ul>
  
</template>

<script>
export default {
    props: ["list"],
    methods: {
        
        del(index){
            //触发父组件的delTest方法
            this.$emit("delTest", index)
        }
    }
}
</script>