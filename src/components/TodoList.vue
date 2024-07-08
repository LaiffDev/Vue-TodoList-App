<script>
export default{
    data(){
        return {
            tasks : [],
            taskInfo : ''
        }
    },
    methods:{
        getTasks(){
            this.taskInfo = this.$refs.taskRef.value
            this.tasks.push(this.taskInfo)
            
            this.$refs.taskRef.value = ''
        },
        deleteTask(){
            //delete task clicked

        }
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
        <button @click="getTasks" class="bg-green-400 p-2 ">Add Task</button>
    </div>
    <div class="w-fit m-auto mt-10 bg-slate-300">
        <p>Todo Task Here : </p>
        <div>
            <ul v-for="task of tasks" :key="task" class="flex gap-5 justify-between items-center m-5 text-center p-5">
                <li>{{ task }}</li>
                <li>
                    <div>
                        <button @click="deleteTask(task)" class="bg-red-500 p-2 text-white">Delete task</button>
                    </div>
                </li>
 
            </ul>
        </div>
    </div>
</template>