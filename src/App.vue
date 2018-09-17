<template>
  <div>
    <myheader></myheader>
    <div>
    <span>Contract Source</span><br />
    <textarea rows="20" cols="50" v-model="source"></textarea><br />
    </div>
    <div>
    <span>Constructor arguments</span><br />
    <input type="text" v-model="args">
    </div>
    <button v-on:click="postRequest()">Deploy</button><br />
    <div>
    [Deploy Status]<span v-if="response">{{response.status}}</span><br />
    <span v-if="response && response.message">{{response.message}}<br /></span>
    [Contract Address] Ethereum: <span v-if="response && response.status == 'success'">{{response.data.ethereum}}</span><br />
    [Contract Address] Qtum: <span v-if="response && response.status == 'success'">{{response.data.qtum}}</span><br />
    </div>
  </div>
</template>

<script>
import myheader from './components/header'
import axios from 'axios'

export default {
  components: {
    myheader
  },
  data () {
    return {
      args: '',
      msg: '',
      posts: [],
      source: '',
      response: ''
    }
  },
  methods: {
    clear () {
      this.msg = ''
    },
    postRequest () {
      axios.post('http://localhost:3002/api/deploy', {
        source: this.source,
        args: this.args
      })
        .then((res) => {
          this.response = res.data
        })
        .catch((res) => {
          console.error(res)
        })
    }
  }
}
</script>
