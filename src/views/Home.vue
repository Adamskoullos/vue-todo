<template>
  <div class="home">
    <div v-if="tasks.length">
      <div v-for="task in tasks" :key="task.id">
        <h1>{{ task.title }}</h1>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'Home',
  components: {},
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
