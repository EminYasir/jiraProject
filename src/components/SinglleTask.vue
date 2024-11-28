<template>
    <div class="task" :class="{complete:task.completed}">
        <div class="actions">
            <h3 @click="showDetail">{{ task.title }}</h3>
            <div>
                <span class="material-symbols-outlined" @click="deleteTask">
                    delete
                </span>
                <router-link :to="{name:'editTask',params:{id:task.id}}" >
                    <span class="material-symbols-outlined">
                        edit
                    </span>
                </router-link>
                <span class="material-symbols-outlined tick" @click="toggleComplete">
                    done
                </span>
            </div>

        </div>
        <div class="details" v-if="isClicked">
            <p>{{ task.details }}</p>
        </div>
    </div>
</template>

<script>


export default {
    name: 'singleTask',
    components: {

    },
    props: ['task'],
    emits: ['delete', 'complete'],
    data() {
        return {
            isClicked: false,
            url: `http://localhost:3000/tasks`
        }
    },
    methods: {
        showDetail() {
            this.isClicked = !this.isClicked;
        },
        deleteTask() {
            fetch(`${this.url}/${this.task.id}`, {
                method: 'DELETE'
            }).then(() => {
                this.$emit('delete', this.task.id)
            }).catch(err => console.log(err))

        },
        toggleComplete() {
            fetch(`${this.url}/${this.task.id}`, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    title: this.task.title,
                    details: this.task.details,
                    completed: !this.task.completed
                })
            })
                .then(() => this.$emit('complete', this.task.id))
                .catch(err => console.log(err))
        },
    }

}
</script>

<style scoped>
.task {
    padding: 10px 20px;
    margin: 20px 0px;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    background: white;
    border-radius: 20px;
    border-left: 8px solid palevioletred;
}
.task.complete {
    border-left: 8px solid lightgreen;
}
.task.complete .tick{
    color: green;
}
h3 {
    cursor: pointer;
}

.actions {
    padding: 15px 0px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.details {
    padding: 20px 0px;
}

.material-symbols-outlined {
    font-size: 25px;
    margin-left: 10px;
    color: gray;
    cursor: pointer;
}

.material-symbols-outlined:hover {
    color: black;
}
</style>