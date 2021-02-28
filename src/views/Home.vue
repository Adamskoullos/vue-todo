<template>
  <div class="home">
    <div v-if="tasks.length">
      <div v-for="task in tasks" :key="task.id">
        <SingleTask :task="task"/>
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
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.tasks = data)
      .catch(err => console.log(err.message))
  }
}
</script>
