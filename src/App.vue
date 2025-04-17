<template>
  <div class="flex flex-col items-center justify-center gap-6 ">
    <div class="bg-white shadow-xl shadow-black mt-20 p-7 rounded-lg">
      <CardInput @add-list="handleAddList" />
      
      <!-- Renderiza cada tarefa individualmente -->
      <div v-for="(task, index) in list" :key="task.text + task.done">
        <UseCard 
  :task="task.text" 
  :done="task.done" 
  :index="index" 
  @remove="removeTask" 
  @done="markTaskDone" 
/>
</div>

    </div>
  </div>
</template>

<script lang="ts" setup>
import UseCard from './components/UseCard.vue';
import CardInput from './components/CardInput.vue';
import { onMounted, watch } from 'vue';
import { ref } from 'vue';

type Task = {
  text: string
  done: boolean
}

const list = ref<Task[]>([]); // Armazena as tarefas como um array de strings
const STORAGE_KEY = 'task-list'

onMounted( () => {
  const saved = localStorage.getItem(STORAGE_KEY)
    if(saved) {
      list.value = JSON.parse(saved)
    }
})

watch(list, (newList) => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(newList))
}, {deep: true})

function handleAddList(newText: string) {
  list.value.push({ text: newText, done: false })
}

function removeTask(index: number) {
  list.value.splice(index, 1)
}

function markTaskDone(index: number) {
  list.value[index].done = !list.value[index].done
}
</script>
