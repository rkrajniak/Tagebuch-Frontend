<template>
<h1>Welcome to Tagebucheintrag</h1>
  <div class="card" style="width: 18rem;">
    <div class="card-body">
      <div class="col" v-for="tagebuch in tagebuecher" :key="tagebuch.id">
      <h5 class="card-title">{{tagebuch.author}}</h5>
      <p class="card-text">{{tagebuch.datum}} {{tagebuch.erlebnis}} {{tagebuch.rating}}</p>
      <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tagebuch-eintrag',
  data () {
    return {
      tagebuecher: []
    }
  },
  mounted () {
    const endpoint = process.env.VUE_APP_BACKEND_BASE_URL + '//api/v1/tagebuch'
    const requestOptions = {
      method: 'GET',
      redirect: 'follow'
    }

    fetch(endpoint, requestOptions)
      .then(response => response.json())
      .then(result => result.forEach(tagebuch => {
        this.tagebuecher.push(tagebuch)
      }))
      .catch(error => console.log('error', error))
  }

}
</script>

<style scoped>

</style>
