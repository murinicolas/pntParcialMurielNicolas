<template>

  <section class="src-componentes-respuestas">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <br>

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Numero de Pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr v-for="(pregunta,index) in preguntas" :key="index">
            <td>{{ pregunta.numero }}</td>
            <td>{{ pregunta.respuestas }}</td>
          </tr>
        </table>
      </div>      

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {
        preguntas: [
          {numero: 1, respuestas: ['b', 'c']},
          {numero: 2, respuestas: ['c']},
          {numero: 3, respuestas: ['e']}
        ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-respuestas {

  }

  .jumbotron {
    background-color: #a0e2ff;
    color: white;
  }
</style>
