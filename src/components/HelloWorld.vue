<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Demo Vue Frontend!!!</h2>
    <div>
      <input type="text" class="nameInput" v-model="name">
      <input type="submit" class="nameSubmit" @click="submit">
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Demo App',
      name: ''
    }
  },
  methods: {
    submit () {
      console.log('name: ' + this.name)
      axios.post('http://localhost:8081/addPerson', {name: this.name}).then(resp => {
        console.log('person added, id: ' + resp.data.id)
      })
    }
  },
  mounted () {
    console.log("mounted...")
    axios.get('http://localhost:8081/hello').then(response  => {
      this.msg = response.data
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
