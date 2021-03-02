<template>
  <div class="home">
    <FilterNav @filter="current = $event" :current="current" />
    <div v-if="tasks.length">
      <div v-for="task in filteredTasks" :key="task.id">
        <SingleTask :task="task" @delete="removeTask" @complete="completeTask" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleTask from '../components/SingleTask.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
  components: { SingleTask, FilterNav },
  data(){
    return{
      tasks: [],
      current: 'all'
    };
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
  },
  computed:{
    filteredTasks(){
      if(this.current === 'complete'){
        return this.tasks.filter(task => task.complete)
      }
      if(this.current === 'open'){       
        return this.tasks.filter(task => !task.complete)
      }
      return this.tasks
    }
  }
}

</script>
