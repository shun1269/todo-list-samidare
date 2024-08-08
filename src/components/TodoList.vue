<script setup lang="ts">
import {ref,computed} from 'vue'

interface Task {
    taskName: string
}

const tasks = ref<Task[]>([

])
const newTaskName = ref('')

interface completedTask {
    compTaskName: string
}

const completedtasks = ref<completedTask[]>([
    
])

const addTask = () => {
    if (newTaskName.value.trim() != ''){
        tasks.value.push({ taskName: newTaskName.value})
        newTaskName.value = ''
    }
}

const changeToCompleted = (index:number) => {
    const pulledtask = tasks.value.splice(index, 1)[0];
    completedtasks.value.push({ compTaskName: pulledtask.taskName });
}

const isAddButtonDisabled = computed(() => {
    return newTaskName.value.trim() == ''
})
</script>

<template>
    <div>TodoList</div>
    <div>未完のタスク</div>
    <ul>
        <li v-for="(task, index) in tasks" :key="task.taskName">
            <div>
                {{ task.taskName }}
                <button @click="changeToCompleted(index)">完了</button>
            </div>
        </li>
    </ul>
    <div>
        <label>
            新しいタスク
            <input v-model="newTaskName" type="text" />
        </label>
        <button @click="addTask" :disabled="isAddButtonDisabled">追加</button>
    </div>
    <div>完了済み</div>
    <ul>
        <li v-for="fintask in completedtasks" :key="fintask.compTaskName">
            <div>
                {{ fintask.compTaskName }}
            </div>
        </li>
    </ul>
</template>

<style>
button:disabled {
    cursor:not-allowed
}
</style>