<template>
  <v-container fluid>
     
    <v-slide-y-transition mode="out-in">
      <Questionnaire students="45"/>
    </v-slide-y-transition>
  </v-container>
</template>

<script>
import Questionnaire from './Questionnaire'
export default {
  name: 'HelloWorld',
  components: {Questionnaire},
  props: {
    msg: String
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
