<template>
<div>
    <h2> Estudiantes: {{students}}</h2>
     <div>{{count}}</div>
     <button v-on:click="click()">
  Enlarge text
</button>
</div>
</template>

<script>


let count = 0;

function click(){
    this.count++;
}


function data(){
return {count} 
}



export default {
  name: 'Questionary',
  props: {
    students: Number
  },
  data,
  methods: {
       click

  }
}
</script>