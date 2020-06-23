<template>
  <div id="app">
    <section class="section">
      <div class="container">
        <div class="field">
          <label class="label">URL</label>
          <div class="control">
            <input class="input" type="text" placeholder="http://" v-model="url">
          </div>
        </div>

        <div class="field">
          <label class="label">Parameter</label>
          <div class="control">
            <textarea class="textarea" placeholder="{json}" v-model="parameter"></textarea>
          </div>
        </div>

        <div class="field">
          <label class="label">Log</label>
          <div class="control">
            <textarea class="textarea" v-model="log"></textarea>
          </div>
        </div>

        <div class="field is-grouped">
          <div class="control">
            <button class="button is-primary" @click="do_post">POST</button>
          </div>
          <div class="control">
            <button class="button">Clear</button>
          </div>
        </div>

      </div>
    </section>
  </div>
</template>

<script>
import Axios from 'axios'

const axios = Axios.create({
  // for cors
  withCredentials: false
})

export default {
  name: 'App',
  components: {
  },
  data: function() {
    return {
      url: 'http://192.168.1.33:9091/lesson/web_reserve',
      parameter: '',
      log: ''
    }
  },
  methods: {
    clear: function() {
      self.log = ''
    },
    do_post: function() {
      var self = this

      self.log = ''

      axios.post(self.url, self.parameter)
        .then(function (res) {
          self.log = JSON.stringify(res)
        })
        .catch(function (error) {
          if (error.response) {
                  self.log = JSON.stringify(error.response.data)
                  console.log(error.response.status)
                  console.log(error.response.statusText)
                  console.log(error.response.headers)
              } else if (error.request) {
                  console.log(error.request)
              } else {
                  console.log(error.message)
              }
              console.log(error.config);
        })
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=M+PLUS+1p:wght@500&display=swap');

$family-sans-serif: 'M PLUS 1p', sans-serif;

@import "bulma/bulma.sass";
</style>
