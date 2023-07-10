<script setup>
import { computed ,inject,ref} from 'vue';
const lists= defineProps({
  list:{
    type:Array
  },
  newList:{
    type:Array
  }
})
const sum=computed(()=>{
const nuy=  lists.list.filter(item=>item.checked === false)
return nuy.length
})
const cler=inject('clerList')
const clerList=()=>{
  cler()
  number.value=0
  meit('id',number.value)
}
const meit=defineEmits(['id'])
const number=ref(0)
const active=(id)=>{
  number.value=id
  meit('id',id)
}
</script>

<template>
  <footer class="footer" v-if="newList.length!==0">
    <span class="todo-count"><strong>{{sum}}</strong> item left</span>
    <ul class="filters">
      <li>
        <a :class="number===0 ? 'selected':''" href="#/" @click="active(0)">All</a>
      </li>
      <li>
        <a :class="number===1 ? 'selected':''" href="#/active" @click="active(1)">Active</a>
      </li>
      <li>
        <a :class="number===2 ? 'selected':''" href="#/completed" @click="active(2)">Completed</a>
      </li>
    </ul>
    <button class="clear-completed" @click="clerList">Clear completed</button>
  </footer>
</template>

<style lang="less" scoped></style>
