<template>
    <h1>Jobs</h1>
    <div v-if="jobs.length">
    <div v-for="job in jobs" :key="job.id" class="job">
        <router-link :to="{ name: 'JobDetails', params: {
            id: job.id }
            }">
            <h2>{{ job.title }}</h2>
        </router-link>
    </div>
    </div>
    <div v-else>
      <p>Loading jobs...</p>
    </div>
</template>

<script>
export default {
    data(){
        return{
          /*
            jobs:[
                { id: 1, title: 'Ux dev', details: 'details1' },
                { id: 2, title: 'Web dev', details: 'details2' },
                { id: 3, title: 'Vue dev', details: 'details3' },
            ]
            */
           jobs: []
        }
    },
    mounted(){
      const url = 'http://localhost:3000/jobs'
      fetch(url)
      .then((res) => res.json())
      .then(data => this.jobs = data)
      .catch((err) => console.log(err.message))
    }
}
</script>

<style>
  .job h2{
    background: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    margin: 10px auto;
    max-width: 600px;
    cursor: pointer;
    color: #444;
  }
  .job h2:hover {
    background: #ddd;
  }
  .job a{
    text-decoration: none;
  }
</style>