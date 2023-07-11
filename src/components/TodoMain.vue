<script setup>
import { ref ,computed,nextTick} from 'vue'; 
const lists= defineProps({
  list:{
    type:Array
  }
})
const emit= defineEmits(['del','checkeds','allCheck','isShow','updateName'])
const del=(id)=>{
  emit('del',id)
}
const checkeds=(id,e)=>{
  // console.log(e.target.checked);
  // console.log(id);
  emit('checkeds',{id:id,checked:e.target.checked})
}
const chengeCheck=(e)=>{
 emit('allCheck', e.target.checked)
}
const ok=computed(()=>{
  return lists.list.every(item=>item.checked===true)
})

const Isshow=(boll,id,i,ok)=>{
if(ok) return alert('已经完成了')
emit('isShow',{isShow:!boll,id:id})
nextTick(()=>{
    inputs.value[i].focus()
  })
}
const name=ref('')
const isName=(e,names)=>{
  name.value=names
  name.value=e.target.value
}
const inputs=ref(null)
const  submit=  (id)=>{
emit('updateName',{id:id,name:name.value})
}
</script>

<template>
  <section class="main" v-if="list.length>0">
    <input id="toggle-all" class="toggle-all" type="checkbox" :checked="ok" @change="chengeCheck"/>
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <li :class="item.checked?'completed':''" v-for="(item,i) in list" :key="item.id" >
        <div class="view" v-show="!item.isShow">
          <input class="toggle" type="checkbox" :checked="item.checked" @input="checkeds(item.id,$event)" />
          <label @dblclick="Isshow(item.isShow,item.id,i,item.checked)">{{item.name}}</label>
          <button class="destroy" @click="del(item.id)"></button>
        </div>
        <input class="edit" ref="inputs" :style="{display:item.isShow?'block':'none'}" :value="item.name" @input="isName($event,item.name)"  @keydown.enter="submit(item.id)" @blur="submit(item.id)"/>
      </li>
    </ul>
  </section>
</template>

<style lang="less" scoped></style>
