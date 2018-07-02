<template>

     <div>
          <div>{{count}}</div>
     <v-flex xs12 sm6 md3>
          <v-text-field
            label="Regular"
          ></v-text-field>
        </v-flex>
    
     <div>{{count}}</div>
      <v-btn
        slot="activator"
        color="purple"
        dark
        v-on:click="click()"
      >
        Click me
      </v-btn>
 
  </div>
</template>

<script>
import * as jsonData from '../JSON/Data.json';

let count = 0;
let estudiantes=0;
let pregunta = jsonData.default.map(function(val){
    val.conocedores =26;
    return val;
});

let data ={ 
    count,
    estudiantes, 
    pregunta,
    valid: false,
     nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters'
      ],};


function create(){
let model = [
    {valor: 1,conocedores: avergeConocedores(1, this.pregunta)},
    {valor: 2,conocedores: avergeConocedores(2,this.pregunta)},
    {valor: 3,conocedores: avergeConocedores(3,this.pregunta)},
    {valor: 4,conocedores: avergeConocedores(4,this.pregunta)},
    {valor: 5,conocedores: avergeConocedores(5, this.pregunta)},

];
 
 calculatepuntuacion(model,this.estudiantes );


function avergeConocedores(indice, pregunta){

   let tamano = pregunta.filter( val=> val.value === indice).length;
   let total =  pregunta.filter( val=> val.value === indice).map(val => val.conocedores).reduce( (accu,val)  => accu + val )/tamano;

   return total;
}
function calculatepuntuacion(model, estudiantes){

let puntuacion0 =((estudiantes) - (model.filter(val=> val.valor===1)[0].conocedores))*0;
let puntuacion1 = ((model.filter(val=> val.valor===1)[0].conocedores) - (model.filter(val=> val.valor===2)[0].conocedores))*1;
let puntuacion2 = ((model.filter(val=> val.valor===2)[0].conocedores) - (model.filter(val=> val.valor===3)[0].conocedores))*2;
let puntuacion3 = ((model.filter(val=> val.valor===3)[0].conocedores) - (model.filter(val=> val.valor===4)[0].conocedores))*3;
let puntuacion4 = ((model.filter(val=> val.valor===4)[0].conocedores) - (model.filter(val=> val.valor===5)[0].conocedores))*4;
let puntuacion5 = ((model.filter(val=> val.valor===5)[0].conocedores))*5;

// eslint-disable-next-line
let totalIndice = (puntuacion1+puntuacion2+puntuacion3+puntuacion4+puntuacion5+puntuacion0)/estudiantes


}

}

function click(){
    this.count++;
}



export default {
  name: 'Questionnaire',
  props: {students: Number},
   methods: {
       click
  },
  data: function(){ return data},
  created: create

}
</script>