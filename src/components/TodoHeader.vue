<script setup>
import { ref } from 'vue'; 
const name=ref('')
const emit=defineEmits(['push'])
const submit=()=>{
  if(!name.value.trim()) return alert('不可以为空')
  emit('push',{id:Date.now(), name:name.value ,checked:false,isShow:false})
  name.value=''
  
}
</script>

<template>
  <header class="header">
    <h1>todos</h1>
    <input class="new-todo" placeholder="What needs to be done?" autofocus   v-model="name" @keydown.enter="submit"/>
  </header>
</template>

<style lang="less" scoped></style>
