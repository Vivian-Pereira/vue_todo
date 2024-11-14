<template>
    <div class="add-task-container">
        <!-- Formulario para agregar una nueva tarea -->
        <div class="add-task-container">
        <h1>Añadir Tarea</h1>
        <div class="input-group">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Añadir nueva tarea" 
                class="task-input"
            />
            <button @click="addTask" class="add-button">Añadir</button>
        </div>
        </div>

        <!-- Lista de tareas -->
        <div class="card">
            <div class="card-body">
                <div v-if="tasks.length > 0">
            <div v-for="task in tasks" :key="task.id">
                <div>
                    <h5 :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.todo }}</h5>
                    <span>{{ task.completed ? 'Completada' : 'Pendiente' }}</span>
                    <button class="add-button" @click="toggleTaskCompletion(task)">
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button class="add-button" @click="deleteTask(task)">Eliminar</button>
                </div>
            </div>
        </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "CombinedView",
    data() {
        return {
            tasks: [],  // Lista de tareas, incluyendo las agregadas manualmente y las de la API
            newTask: "",  // Almacena la tarea nueva
        };
    },
    created(){
        this.fetchTasks();
    },
    methods: {
        // Obtiene las tareas desde la API externa
        fetchTasks() {
            axios
                .get("https://dummyjson.com/todos")
                .then((response) => {
                    this.tasks = response.data.todos;
                })
                .catch((error) => {
                    console.error(error);
                });
        },

        // Cambia el estado de una tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Agrega una tarea nueva a la lista de tareas
        addTask() {
            if (this.newTask.trim() !== "") {
                const newTask = {
                    id: Date.now(), // ID único basado en la fecha actual
                    todo: this.newTask,
                    completed: false
                };
                this.tasks.push(newTask); // Añade la nueva tarea a la lista
                this.newTask = ""; // Limpia el campo de entrada
            }
        },

        // Elimina una tarea de la lista
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
.container {
    max-width: 800px;
}

.card {
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

.input-group {
    display: flex;
}

.list-group-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.add-task-container {
    padding: 20px;
    max-width: 400px;
    margin: 0 auto;
}

.input-group {
    display: flex;
    margin-bottom: 10px;
}

.task-input {
    flex-grow: 1;
    padding: 8px;
    margin-right: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.add-button {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
}

.task-list {
    margin-top: 20px;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #eee;
}

.completed {
    text-decoration: line-through;
    color: gray;
}
</style>