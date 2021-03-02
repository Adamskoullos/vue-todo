<template>
    <div class="task" :class="{ complete: task.complete }">
        <div class="actions" >
            <h2 @click="showDetails">{{ task.title }}</h2>
            <div class="icons">
                <router-link :to="{ name: 'EditTask', params: { id: task.id } }">
                    <span class="material-icons">edit</span>
                </router-link>
                <span class="material-icons" @click="deleteTask">delete</span>
                <span class="material-icons" @click="toggleComplete">done</span>
            </div>
        </div>
        <div class="details" v-if="showTaskDetails">
            <p>{{ task.details }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['task'],
    data(){
        return{
            showTaskDetails: false,
            uri: 'http://localhost:3000/tasks/' + this.task.id
        }
    },
    methods:{
        showDetails(){
            this.showTaskDetails = !this.showTaskDetails
        },
        deleteTask(){
            fetch(this.uri, { method: 'delete' })
                .then(() => this.$emit('delete', this.task.id))
                .catch(err => console.log(err.message))
        },
        toggleComplete(){
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({complete: !this.task.complete})
            }).then(() => {
                this.$emit('complete', this.task.id)
            }).catch(err => console.log(err.message))
        }
    }
}
</script>

<style scoped>

.task {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    border-left: 4px solid #e90074;
  }
  h2 {
    cursor: pointer;
  }
  .actions{
      display: flex;
      align-items: center;
      justify-content: space-between;
  }
  .material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  }
  .material-icons:hover {
    color: #777;
  }
  .complete{
    border-left: 4px solid rgb(7, 177, 7); 
}
</style>