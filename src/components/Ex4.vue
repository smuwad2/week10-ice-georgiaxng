<script>
export default {
    data() {
        return {
            desc: '',
            deadline: '',
            taskList: []
        }
    },
    methods: {
        add() {
            if (this.desc && this.deadline) {
                this.taskList.push({ desc: this.desc, deadline: this.deadline });
                this.desc = '';
                this.deadline = '';
            }
        },
        remove(index) {
            this.taskList.splice(index, 1);
        }
    }
}
</script>

<template>
    <div class="mb-3">
        <label for="desc" class="form-label">Task</label>
        <input type="text" class="form-control" id="desc" v-model='desc' placeholder="task">
    </div>
    <div class="mb-3">
        <label for="deadline" class="form-label">Deadline</label>
        <input type="date" class="form-control" id="deadline" v-model='deadline' placeholder="deadline">
    </div>

    <button type="button" @click="add" class="btn btn-primary">Add New Task</button>
    <hr>

    <!-- Display tasks -->
    <div v-for="(task, index) in taskList" :key="index" class="card mb-2 p-2">
        <p>{{ task.desc }}</p>
        <small>Deadline: {{ task.deadline }}</small>
        <button type="button" class="btn btn-success btn-sm mt-2" @click="remove(index)">Done</button>
    </div>
</template>

<style scoped>
.card {
    border: 1px solid #ccc;
    border-radius: 4px;
}
</style>
