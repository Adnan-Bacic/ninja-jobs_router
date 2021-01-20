<template>
<div v-if="job">
  <h1>{{ job.title }}</h1>
  <p>The job id is {{ id }}</p>
  <p>{{ job.details }}</p>
</div>
<div v-else>
    <p>Loading job details...</p>
</div>
</template>

<script>
export default {
    props:{
        id: Number
    },
    //since we define props in the router we can also do without data()
    /*
    data(){
        return{
            id: this.$route.params.id
        }
    }
    */
   data(){
       return{
           job: null
       }
   },
   mounted(){
      const url = `http://localhost:3000/jobs/${this.id}`
      fetch(url)
      .then((res) => res.json())
      .then(data => this.job = data)
      .catch((err) => console.log(err.message))
    }
}
</script>

<style>

</style>