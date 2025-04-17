<template>
  <div
    class="p-4 rounded-sm shadow-md mt-6 flex justify-between items-center 
    transition-all duration-300 ease-in-out" 
    :style="{ backgroundColor: done ? '#48bb78' : '#edf2f7' }"
  >
    <p
      class="text-lg text-black font-normal transition-all duration-300 ease-in-out"
      :style="{ textDecoration: done ? 'line-through' : 'none', opacity: done ? 0.5 : 1 }"
    >
      {{ task }}
    </p>
    <!-- Exibe a tarefa individual -->
    <div class="flex gap-2">
      <!-- Botão confirmar -->
      <button
        class="bg-green-600 text-white px-2 py-1 rounded hover:bg-green-700 hover:scale-105 transition-transform duration-300 ease-in-out cursor-pointer"
        @click="markAsDone"
      >
        ✅
      </button>
      <!-- Botão excluir -->
      <button
        class="bg-red-600 text-white px-2 py-1 rounded hover:bg-red-700 cursor-pointer hover:scale-105 transition-transform duration-300 ease-in-out"
        @click="deleteTask"
      >
        🗑️
      </button>
    </div>
  </div>
</template>

<script lang="ts" setup>
defineOptions({
  name: "UseCard",
});

const props = defineProps<{
  task: string; // Espera uma tarefa individual (string)
  index: number;
  done: boolean;
}>();

const emit = defineEmits<{
  (e: "remove", index: number): void;
  (e: "done", index: number): void;
}>();

function markAsDone() {
  emit("done", props.index);
}

function deleteTask() {
  emit("remove", props.index);
}
</script>
