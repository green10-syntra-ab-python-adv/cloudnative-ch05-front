<template>
  <div class="HelloCh05">
        <form @submit.prevent="getIdToLookup">
        <input type="text" placeholder="id?" v-model="idToLookup" name="idToLookup">
    </form>

      <br/>

    <div v-if=" info == 'error' ">
        Unfortunately, something went wrong<br/><br/>
    </div>
    <div v-else  >
        We have read the <strong>entry with id </strong> {{ info.user_details[0].id }} from the backend:
        <ul>
            <li> <strong>Name: </strong> {{ info.user_details[0].name }} </li>
            <li> <strong>E-mail: </strong> {{ info.user_details[0].email }} </li>
            <li> <strong>Username: </strong> {{ info.user_details[0].username }} </li>
            <li> <strong>Password: </strong> {{ info.user_details[0].password}} </li>
        </ul>
    </div>
    <div>
      <strong>Status: </strong> {{ status }}
    </div>
    <div v-if= " info == 'error' " >
      <strong>Error: </strong> {{ error }}
    </div>
  </div>
</template>

<script>
    import * as axios from "axios";

    export default {
        name: "HelloCh05",
        data () {
            return {
                idToLookup: '',
                theUrl: '',
                info: null,
                status: null,
                error: null
            }
        },
        mounted () {
            this.idToLookup = '5'
            this.getIdToLookup()
        },
        methods: {
            getIdToLookup() {
                this.theUrl = 'http://localhost:5000/api/v1/users/' + this.idToLookup
                axios
                    .get(this.theUrl)
                    .then(response => (this.info = response.data,
                                        this.status = response.status) )
                    .catch(error => (this.info = "error",
                                        this.status = error.response.status,
                                        this.error = error.response.data.error ) )
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
