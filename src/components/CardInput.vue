<template>
        <label for="">
          <input 
          type="text" 
          placeholder="O que tenho que fazer..." 
          class="bg-white p-2 mr-2 rounded-lg border-black border-2 w-90"
          v-model="localList"
          >
          <button 
          class="bg-green-800 p-2 ml-20 text-white font-bold rounded-lg cursor-pointer hover:scale-105 transition-transform duration-300 ease-in-out hover:bg-green-600"
          @click="emitList"
          >ADICIONAR</button>
        </label>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
      defineOptions({
        name: "CardInput"
      }) 

      const emit = defineEmits<{
        (e: 'add-list', value: string): void
      }>()

      const localList = ref('')

      function emitList() {
        if(localList.value.trim()) {
          emit('add-list', localList.value)
          localList.value = ''
        }
      }
</script>