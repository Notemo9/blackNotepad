<script setup>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
import {ref,watch,provide} from 'vue'
const list =ref(JSON.parse(localStorage.getItem('list'))||[])
const fakeList=ref(list.value)
const pushList=(e)=>{
  console.log(e);
list.value.push(e)
}
// 删除
const del=(e)=>{
  console.log('删了')
list.value= list.value.filter(item=>item.id!==e)
}
// 点击check
const checked=(e)=>{
  list.value.forEach(item=>{
    if(item.id===e.id){
      item.checked=e.checked
      console.log(item);
    }
  })
}
watch(list,(newVal)=>{
  localStorage.setItem('list',JSON.stringify(list.value))
  fakeList.value=list.value
},{
  immediate:true,
  deep:true
})
const allCheck=(e)=>{
  list.value.forEach(item=>item.checked=e)
}

const clerList=()=>{
  list.value= list.value.filter(item=>item.checked!==true)
}
provide('clerList',clerList)

const id=(id)=>{
  if(id===1){
    fakeList.value= list.value.filter(item=>item.checked!==true)
  }else if(id===2){
    fakeList.value= list.value.filter(item=>item.checked===true)
  }else{
    fakeList.value=list.value
  }
}

const isShow=(e)=>{
  console.log(e);
  list.value.forEach(item=>{
  if(item.id===e.id){
    item.isShow=e.isShow
  }
 })
}

const updateName=(e)=>{
  console.log(e.name);
  list.value.forEach(item=>{
  if(item.id===e.id){
    item.name=e.name
    item.isShow=false
  }
  })
}
</script>

<template>
  <section class="todoapp">
    <TodoHeader  @push="pushList"></TodoHeader>
    <TodoMain :list="fakeList" @del="del" @checkeds="checked" @allCheck="allCheck" @isShow="isShow" @updateName="updateName"></TodoMain>
    <TodoFooter :list="fakeList" @id="id" :newList="list"></TodoFooter>
  </section>
</template>

<style></style>
