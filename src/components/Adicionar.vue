<template>
  <div class="container">
    <div class="input-adicionar">
      <input v-model="newTask" id="" placeholder="Nova Tarefa" @keyup.enter="addTask">
      <button @click="addTask"><i class="fa-solid fa-plus"></i></button>
    </div>

    <div class="lista-tarefas">
      <ul>
        <li v-for="task in tasks" :key="task.id">

          <div v-if="editingId === task.id" class="salvar">
            <input v-model="editingText" id="">
            <button @click="saveEdit(task.id)" class="salvar-button"><i class="fa-solid fa-bookmark"></i></button>
            <button @click="cancelEdit" class="Cancelar-button"><i class="fa-regular fa-circle-xmark"></i></button>
          </div>

          <div v-else class="opcoes">
            <span>{{ task.texto }}</span>
            <button @click="startEdit(task)" class="editar"><i class="fa-solid fa-pen-to-square"></i></button>
            <button @click="removeTask(task.id)" class="deletar"><i class="fa-solid fa-trash"></i></button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'

const newTask = ref('')
const tasks = ref([])
const editingId = ref(null)
const editingText = ref('')

onMounted(() => {
  const salvo = localStorage.getItem('tasks')
  if (salvo) {
    tasks.value = JSON.parse(salvo)
  }
})

watch(tasks, (novoValor) => {
  localStorage.setItem('tasks', JSON.stringify(novoValor))
}, {deep: true})

function addTask() {
  if (!newTask.value.trim()) return

  tasks.value.push({
    id: Date.now(),
    texto: newTask.value,
  })

  newTask.value = ''
}

function removeTask(id) {
  tasks.value = tasks.value.filter(task => task.id !== id)
}

function startEdit(task) {
  editingId.value = task.id
  editingText.value = task.texto
}

function saveEdit(id) {
  const task = tasks.value.find(t => t.id === id)
  if (task) {
    task.texto = editingText.value
  }
  editingId.value = null
  editingText.value = ''
}

function cancelEdit() {
  editingId.value = null
  editingText.value = ''
}
</script>

<style scoped>
.container {
  text-align: center;
  margin: 2rem;
  margin-top: 6.8rem;
}

.input-adicionar {
  margin-bottom: 2rem;
}

.input-adicionar input {
  padding: 1.3rem 8rem 1.3rem 1.2rem ;
  border-radius: 2rem;
  border: none;
  font-size: 1rem;
  text-align: start;
}

.input-adicionar button {
  padding: 0.8rem 1rem;
  border-radius: 2rem 2%;
  border: none;
  background-color: var(--background-icon);
  color: var(--color-icon);
  cursor: pointer;
  margin-left: 0.5rem;
  transition: 0.5s ease;
}

.input-adicionar i {
  font-size: 1.2rem;
}

.input-adicionar button:hover {
  opacity: 0.5;
  border: 2px solid var(--color-icon);
}

.lista-tarefas {
  margin: 0 auto;
}

.lista-tarefas ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(252px, 380px));
  justify-content: center;
  gap: 1rem;
}

.lista-tarefas li {
  border: 1px solid var(--background-box-list);
  border-radius: 1rem;
  padding: 0.8rem 1.2rem;
  color: var(--color-font);
}

.opcoes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.5rem;
}

.opcoes span {
  flex: 1;
  min-width: 0;
  text-align: left;
  color: var(--color-list);
  font-size: 1.2rem;
  overflow-wrap: break-word;
}

.opcoes button {
  display: flex;
  background: transparent;
  border: none;
  cursor: pointer;
  flex-shrink: 0;
}

.opcoes button:hover {
  color: #000;
}

.deletar i{
  font-size: 1.2rem;
  color: var(--color-button-options);
  background-color: var( --background-button-delet);
  padding: 0.5rem;
  border-radius: 30%;
  cursor: pointer;
  transition: all 0.5s ease;
}

.editar i{
  font-size: 1.2rem;
  color: var(--color-button-options);
  background-color: var( --background-button-edit);
  padding: 0.5rem;  
  border-radius: 30%;
  cursor: pointer;
  transition: all 0.5s ease;
}

.editar i:hover,
.deletar i:hover{
  opacity: 0.3;
}

.salvar input{
  color: red;
  border: none;
  border-radius: 2rem;
  padding: 0.4rem 2rem;
}

.salvar button{
  color: var( --color-button-options);
  margin:0.2rem;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.salvar-button i{
  font-size: 1.2rem;
  color: var(--color-button-options);
  background-color: var( --background-button-edit);
  padding: 0.5rem;  
  border-radius: 30%;
  cursor: pointer;
  transition: all 0.5s ease;
}

.Cancelar-button i{
 font-size: 1.2rem;
  color: var(--color-button-options);
  background-color: var( --background-button-delet);
  padding: 0.5rem;
  border-radius: 30%;
  cursor: pointer;
  transition: all 0.5s ease;
}
</style>