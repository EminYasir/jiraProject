<template>
  <div>
    <FilterTask :current="current" @updateFilter="updateFilter" />
    <div class="home" v-if="tasks.length">
      <div v-for="task in filteredTasks" :key="task.id">
        <SinglleTask :task="task" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SinglleTask from '../components/SinglleTask.vue'
import FilterTask from '../components/FilterTask.vue'

export default {
  name: 'HomeView',
  components: {
    SinglleTask,
    FilterTask
  },
  data() {
    return {
      tasks: [],
      current: 'all'
    }
  },
  methods: {
    handleDelete(id) {
      this.tasks = this.tasks.filter(task => { return task.id !== id })
    },
    handleComplete(id) {
      let myTask = this.tasks.find(task => {
        return task.id === id
      })
      myTask.completed = !myTask.completed
    },
    updateFilter(filter) {
      this.current = filter
    }
  },
  mounted() {// this is a lifecycle hook that runs after the component has been mounted to the DOM
    fetch('http://localhost:3000/tasks')
      .then(response => response.json())
      .then(data => this.tasks = data)
      .catch(err => console.log(err))

  },
  computed: {
    filteredTasks() {
      if (this.current === 'completed') {
        return this.tasks.filter(task => task.completed)
      } 
      if (this.current === 'continue') {
        return this.tasks.filter(task => !task.completed)
      }
      return this.tasks;
    }
  }
}
</script>

<style scoped></style>