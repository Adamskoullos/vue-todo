<template>
  <form @submit.prevent="submitUpdate">
        <label>Title:</label>
        <input type="text" v-model="title" required>
        <label>Details:</label>
        <textarea v-model="details" required></textarea>
        <button>Update task</button>
    </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
        return{
            title: '',
            details: '',
            uri: 'http://localhost:3000/tasks/' + this.id
        }
    },
    mounted(){
        fetch(this.uri)
            .then(res => res.json())
            .then(data => {
                this.title = data.title
                this.details = data.details
            })
    },
    methods:{
        submitUpdate(){
            let task = {
                title: this.title,
                details: this.details,
            }
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(task) 
            }).then(() => {
                this.$router.push('/')
            }).catch(err => console.log(err.message))
        }
    }
}
</script>

<style>

</style>