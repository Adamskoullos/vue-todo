<template>
  <div class="home">
    <div v-if="tasks.length">
      <div v-for="task in tasks" :key="task.id">
        <SingleTask :task="task" @delete="removeTask" @complete="completeTask" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleTask from '../components/SingleTask.vue'

export default {
  name: 'Home',
  components: { SingleTask },
  data(){
    return{
      tasks: []
    }
  },
  mounted(){
    fetch('http://localhost:3000/tasks')
      .then(res => res.json())
      .then(data => this.tasks = data)
      .catch(err => console.log(err.message))
  },
  methods: {
    removeTask(id){
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id
      })
    },
    completeTask(id){
      this.tasks.forEach(task => {
        if(task.id == id){
          task.complete = !task.complete
        }
    //Same outcome using the find() method
      //let obj = this.tasks.find(task => {
      //  return task.id === id
      //})
      //obj.complete = !obj.complete
      })
    }
  }
}
</script>
