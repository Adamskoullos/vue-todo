<template>
    <div class="task">
        <div class="actions" @click="showDetails">
            <h2>{{ task.title }}</h2>
            <div class="icons">
                <span class="material-icons">edit</span>
                <span class="material-icons">delete</span>
                <span class="material-icons">done</span>
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
            showTaskDetails: false
        }
    },
    methods:{
        showDetails(){
            this.showTaskDetails = !this.showTaskDetails
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
</style>