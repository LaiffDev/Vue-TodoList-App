<script>
export default{
    data(){
        return {
            tasks : [],
            taskInfo : '',
            selectedPriority : ''
        }
    },
    methods:{
        getTasks() {
            this.taskInfo = this.$refs.taskRef.value
            
            if (this.taskInfo && this.selectedPriority) {
                this.tasks.push({ description: this.taskInfo, priority: this.selectedPriority })
                localStorage.setItem('tasks', JSON.stringify(this.tasks))
            }
            
            this.$refs.taskRef.value = ''
            this.selectedPriority = ''
        },
        saveTasks() {
            const savedTasks = localStorage.getItem('tasks')
            if (savedTasks) {
                this.tasks = JSON.parse(savedTasks)
            }
        },
        deleteTask(index) {
            const spliced = this.tasks.splice(index, 1)
            localStorage.setItem('tasks', JSON.stringify(this.tasks))
            console.log("deleted task: ", spliced)
        }
    },
    mounted(){
        this.saveTasks()
    }

}
</script>

<template>
    <div class="w-fit m-auto mb-10 text-center">
        <h2 class="font-bold">Add your todo list</h2>
        <span>This todo-app is a simple app to demonstrate what has been learnt in VueJS</span>
    </div>
    <div class="flex justify-center gap-5">
        <input type="text" ref="taskRef" class="border border-black p-2">
        <select name="priority" id="priority" v-model="selectedPriority" required>
            <optgroup label="Priorities">
                <option value="" disabled selected>Choose a priority</option>
                <option value="high">High priority</option>
                <option value="medium">Medium priority</option>
                <option value="low">Low priority</option>
            </optgroup>
        </select>
        <button @click="getTasks" class="bg-green-500 p-2 text-white">Add Task</button>
    </div>
    <div class="w-full m-auto mt-10 p-3">
        <p class=" text-center">Todo Tasks : </p>
        <div>
            <ul v-for="(task,index) of tasks" :key="index" class="flex gap-5 justify-between items-center text-center p-5">
                <div class="bg-black rounded-full text-orange-500 flex gap-20 justify-between items-center w-full p-5">
                    <p class="text-black" :class="{'high' : task.priority === 'high', 'medium' : task.priority === 'medium', 'low' : task.priority === 'low'}"></p>
                    <p class="font-bold">{{ task.description }}</p>
                    <div class="gap-5 flex">
                        <button @click="deleteTask(index)" class="bg-red-500 p-2 text-white rounded-full">Delete task</button>
                        <!-- <button  class="bg-blue-500 p-2 text-white rounded-full">Edit task</button> -->
                    </div>
                </div>
            </ul>
        </div>
    </div>
</template>

<style scoped>
    .high{
        background-color: red;
        padding: 2px;
        border-radius: 100%;
        color: white;
        width:20px;
        height: 20px;
    }
    .medium{
        background-color: orange;
        padding: 2px;
        border-radius: 100%;
        color: white;
        width:20px;
        height: 20px;
    }
    .low{
        background-color: royalblue;
        padding: 2px;
        border-radius: 100%;
        color: white;
        width:20px;
        height: 20px;
    }
</style>