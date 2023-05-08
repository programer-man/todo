<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{remainder}}</strong></span>
    <ul class="filters" @click="change">
      <li >
        <a  href="javascript:;" :class="{selected: isSel === 'all'}" @click="isSel = 'all'" >全部</a>
      </li>
      <li >
        <a href="javascript:;" :class="{selected: isSel === 'no'}" @click="isSel = 'no' ">未完成</a>
      </li>
      <li >
        <a href="javascript:;" :class="{selected: isSel === 'yes'}" @click="isSel = 'yes'">已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="cleanY">清除已完成</button>
  </footer>
</template>

<script>
export default {
    props: ['arr'],
    data(){
        return{
            isSel: 'all',
            status: ['all', 'no', 'yes']
        }
    },
    computed: {
        remainder:{
            set(){},
            get(){
                return this.arr.length
            },
        }
    },
    methods: {
        change(){
            this.$emit('changeList', this.isSel)   
        },
        cleanY(){
            this.$emit('cleanY')
        }
    },


}
</script>