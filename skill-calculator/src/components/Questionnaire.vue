<template>
    <v-flex >
      <v-card>

        <v-card-title primary-title>
          <div>
            <h3 class="headline mb-0">Kangaroo Valley Safari</h3>
            <div>Located two hours south of Sydney in the <br>Southern Highlands of New South Wales, ...</div>
          </div>
        </v-card-title>

         <v-list three-line>
          <template v-for="(item, index) in preguntas">
       
            <v-list-tile  
              :key="item.Question"
              avatar
              @click=""
            >
              <v-list-tile-avatar>
                <i class="material-icons">
favorite
</i>
              </v-list-tile-avatar>

              <v-list-tile-content>
                <v-list-tile-title v-html="item.Question"></v-list-tile-title>
                <v-list-tile-sub-title v-html="item.conocedores"></v-list-tile-sub-title>
             
              </v-list-tile-content>
              <v-list-tile-content>
               
                  <v-flex xs12 sm6 md3>
          <v-text-field
            label="Total"
            v-model="item.conocedores"
          ></v-text-field>
        </v-flex>
              </v-list-tile-content>
            </v-list-tile>
          </template>
        </v-list>

        <v-card-actions>
           <v-btn
        color="purple"
        dark
        v-on:click="calcular()"
      >
        Calcular
      </v-btn>
          {{indiceClase}}
        </v-card-actions>
       
      </v-card>
    </v-flex>
</template>

<script>
import * as jsonData from "../JSON/Data.json";
let indiceClase = 0;
let estudiantes = 26;
let preguntas = jsonData.default.map(function(val) {
  val.conocedores = 26;
  return val;
});

let data = {
  indiceClase,
  estudiantes,
  preguntas
};

function create() {
 //alert("ok");
}

function calcular() {
 let model = [
    { valor: 1, conocedores: avergeConocedores(1, this.preguntas) },
    { valor: 2, conocedores: avergeConocedores(2, this.preguntas) },
    { valor: 3, conocedores: avergeConocedores(3, this.preguntas) },
    { valor: 4, conocedores: avergeConocedores(4, this.preguntas) },
    { valor: 5, conocedores: avergeConocedores(5, this.preguntas) }
  ];

 this.indiceClase =  calculatepuntuacion(model, this.estudiantes);

  function avergeConocedores(indice, preguntas) {
    let tamano = preguntas.filter(val => val.value === indice).length;
    let total =
      preguntas
        .filter(val => val.value === indice)
        .map(val => val.conocedores)
        .reduce((accu, val) => accu + val) / tamano;

    return total;
  }
  function calculatepuntuacion(model, estudiantes) {
    let puntuacion0 =
      (estudiantes - model.filter(val => val.valor === 1)[0].conocedores) * 0;
    let puntuacion1 =
      (model.filter(val => val.valor === 1)[0].conocedores -
        model.filter(val => val.valor === 2)[0].conocedores) *
      1;
    let puntuacion2 =
      (model.filter(val => val.valor === 2)[0].conocedores -
        model.filter(val => val.valor === 3)[0].conocedores) *
      2;
    let puntuacion3 =
      (model.filter(val => val.valor === 3)[0].conocedores -
        model.filter(val => val.valor === 4)[0].conocedores) *
      3;
    let puntuacion4 =
      (model.filter(val => val.valor === 4)[0].conocedores -
        model.filter(val => val.valor === 5)[0].conocedores) *
      4;
    let puntuacion5 = model.filter(val => val.valor === 5)[0].conocedores * 5;

    // eslint-disable-next-line
    let totalIndice =
      (puntuacion1 +
        puntuacion2 +
        puntuacion3 +
        puntuacion4 +
        puntuacion5 +
        puntuacion0) /
      estudiantes;
       return totalIndice;
  }
 
}

export default {
  name: "Questionnaire",
  props: { students: String },
  methods: {
    calcular
  },
  data: function() {
    return data;
  },
  created: create
};
</script>