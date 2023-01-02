<template>
    <div class="container">
        <h2 class="text-center mt-5">My to-do list</h2>

        <!-- Enter task and submit -->

        <div class="d-flex wid">
            <input v-model="task" type="text" class="form-control"
             id="enterTask" placeholder="Enter task" @keydown.enter="submitTask">
            <b-button @click="submitTask" squared variant="info" id="subbtn">Submit</b-button>
        </div>

        <!-- Table of tasks -->

        <!-- table header -->

        <table class="table table-bordered mt-5 wid">
            <thead>
            <tr>
            <th scope="col">Task</th>
            <th scope="col" class="text-center">status</th>
            <th scope="col" class="text-center">edit</th>
            <th scope="col" class="text-center">delete</th>
            </tr>
        </thead>

        <!-- table body -->

        <tbody>

        <!-- Task name -->

            <tr v-for="(task, index) in tasks" :key="index">
            <th>
                <span :class="{'done': task.status === 'done'}">
                    {{task.name}}
                </span>
            </th>

        <!-- Task status -->

            <td class="pointer text-center">
                <span @click="changeStatus(index)" :class="{'text-danger': task.status ==='to-do',
                'text-warning': task.status === 'in-progress',
                'text-success': task.status === 'done'}">
                    {{task.status}}
                </span>
            </td>
            <td>

        <!-- Edit task -->

                <div class="text-center pointer" @click="editTask(index)">
                    <span class="fa fa-pen"></span>
                </div>
            </td>

        <!-- Delete task -->

            <td>
                <div class="text-center pointer" @click="deleteTask(index)">
                    <span class="fa fa-trash"></span>
                </div>
            </td>
            </tr>
        </tbody>

        </table>

    </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    data(){
        return {
            task: '',
            editedTask: -1,
            availableStatuses: ['to-do', 'in-progress', 'done'],
            tasks: [
                {
                    name: 'go to gym',
                    status: 'to-do'
                },
                {
                    name: 'practice ts',
                    status: 'in-progress'
                }
            ]
        }
        interface KeyboardEvent {
            enterKey: boolean;
         }
    },


    methods: {
        submitTask(task: string):any{
            if (this.task.length === 0) return;

            if(this.editedTask == -1){
                this.tasks.push({
                    name: this.task,
                    status: 'to-do'
                })
            }
            else{
                 this.tasks[this.editedTask].name = this.task;
                 this.editedTask = -1;
            }
            this.task = '';
        },

        deleteTask(index: number){
            this.tasks.splice(index, 1);
        },

        editTask(index: number){
            this.task = this.tasks[index].name;
            document.getElementById("enterTask")?.focus();
            this.editedTask = index;
        },

        changeStatus(index: number){
            let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
            if(++newIndex > 2) newIndex = 0;
            this.tasks[index].status = this.availableStatuses[newIndex];
            }
    }
})
</script>

<style>
    .wid{
        max-width: 800px;
        margin:20px auto;
    }
    
    .pointer{
        cursor: pointer;
    }

    .done{
        text-decoration: line-through;
    }

    thead>tr{
        background-color: rgb(212, 238, 232);
    }

    tbody>tr:hover{
        background-color:rgb(240, 240, 240);
    }

</style>