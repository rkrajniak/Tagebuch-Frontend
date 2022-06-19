<template>
<h1>Welcome to Tagebucheintrag</h1>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-md-4 g-4">
      <div class="col" v-for="tagebuch in tagebuecher" :key="tagebuch.id">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">{{ tagebuch.author }}</h5>
            <p class="card-text">
              {{ tagebuch.erlebnis }} {{ tagebuch.datum }} {{ tagebuch.rating }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tagebuch-eintrag',
  data () {
    return {
      tagebuecher: [
        {
          id: 1,
          author: 'max',
          datum: '2022-06-19',
          erlebnis: 'test',
          rating: 'GUT'
        }

      ]
    }
  },
  mounted () {
    const endpoint = process.env.VUE_APP_BACKEND_BASE_URL + '/api/v1/tagebuch'
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
