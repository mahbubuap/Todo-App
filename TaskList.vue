<script setup>
import { ref } from 'vue';

const tasks = ref([
    { name: 'Task 1', time: 60 },
    { name: 'Task 2', time: 75 },
    
]);

const isAddTaskPopupOpen = ref(false);

const newTask = ref({
    name: '',
    time: 0,
});

const openAddTaskPopup = () => {
    isAddTaskPopupOpen.value = true;
};

const closeAddTaskPopup = () => {
    isAddTaskPopupOpen.value = false;
    newTask.value = { name: '', time: 0 };
};

const addTask = () => {
    if (newTask.value.name && newTask.value.time > 0) {
        tasks.value.push({ ...newTask.value });
        closeAddTaskPopup();
    } else {
        alert('Please fill out all fields.');
    }
};

const removeTask = (index) => {
    tasks.value.splice(index, 1);
};
</script>

<template>
    <div class="container mx-auto p-4">
        <h1 class="text-3xl font-bold mb-4">TASK LIST</h1>

        <div v-if="tasks.length === 0" class="text-gray-500">
            No tasks available. Add a task to get started.
        </div>

        <div v-else>
            <div v-for="(task, index) in tasks" :key="index"
                class="flex items-center space-x-4 my-2 bg-white p-4 rounded-md shadow-md hover:shadow-lg transition duration-300">
                <div class="flex-grow">
                    {{ task.name }} - {{ task.time }} minutes
                </div>
                <button @click="removeTask(index)"
                    class="bg-red-500 text-white px-3 py-1 rounded-md hover:bg-red-600 transition duration-300">Remove</button>
            </div>
        </div>

        <button @click="openAddTaskPopup"
            class="mt-4 bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition duration-300">
            Add Task
        </button>

        <div v-if="isAddTaskPopupOpen"
            class="fixed top-0 left-0 w-full h-full bg-gray-800 bg-opacity-50 flex items-center justify-center">
            <div class="bg-white p-4 rounded-md shadow-md w-96">
                <h2 class="text-xl font-bold mb-4">Add Task</h2>
                <form @submit.prevent="addTask">
                    <div class="mb-4">
                        <label for="taskName" class="block text-sm font-medium text-gray-600 mb-1">Task Name</label>
                        <input v-model="newTask.name" type="text" id="taskName" name="taskName"
                            class="mt-1 p-2 w-full border rounded-md focus:outline-none focus:ring focus:border-blue-300">
                    </div>
                    <div class="mb-4">
                        <label for="taskTime" class="block text-sm font-medium text-gray-600 mb-1">Time (minutes)</label>
                        <input v-model.number="newTask.time" type="number" id="taskTime" name="taskTime"
                            class="mt-1 p-2 w-full border rounded-md focus:outline-none focus:ring focus:border-blue-300">
                    </div>
                    <button type="submit"
                        class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition duration-300">Add
                        Task</button>
                </form>
                <button @click="closeAddTaskPopup" class="mt-2 text-gray-600">Cancel</button>
            </div>
        </div>
    </div>
</template>



<style scoped>   </style>
