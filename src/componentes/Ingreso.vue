<template>

  <section class="src-componentes-ingreso">
    <div class="jumbotron">
      <h2>Ingreso de Gastos</h2>
      <hr>

      <vue-form :state="formstate" @submit.prevent="enviar()">
        
        <!-- Campo nombre -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input type="text" id="nombre" v-model="formData.nombre" required name="nombre" autocomplete="off" class="form-control" />
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo no puede tener menos de {{nombreMinLength}} caracteres y no más de
              {{nombreMaxLength}} caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no admite espacios intermedios.
            </div>
          </field-messages>
        </validate>
        <br>

        <!-- Campo descripcion -->
        <validate tag="div">
          <label for="descripcion">Descripción</label>
          <input type="text" id="descripcion" v-model="formData.descripcion" required name="descripcion" autocomplete="off" class="form-control" />
    
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>
        <br>
        
        <!-- Campo importe -->
        <validate tag="div">
          <label for="importe">Importe</label>
          <input type="number" id="importe" v-model.number="formData.importe" required name="importe" autocomplete="off" class="form-control" />
    
          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>

        <br>

        <button class="btn btn-success my-3" :disabled="formstate.$invalid"  @click="actualizar()"  type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>

      <!-- Tabla para representar los datos ingresados -->
      <h2>Detalle de Gastos</h2>
      <br>

      <h5>Presupuesto</h5>
      <input type="text" v-model="presupuesto"> <br>

      <br>

      <div v-if="gastos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Descripción</th>
            <th>Importe</th>
            <th>Fecha</th>
          </tr>
          <tr v-for="(gasto,index) in gastos" :key="index">
            <td>{{ gasto.nombre }}</td>
            <td>{{ gasto.descripcion }}</td>
            <td>{{ gasto.importe }}</td>
            <td>{{ gasto.fecha }}</td>
          </tr>
          <tr :style="{color: analizarSaldo() }">
            <td></td>
            <td>TOTAL:</td>
            <td> {{total}} </td>
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-info">No hay gastos ingresados</h3>

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-ingreso',
    props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        gastos : [],
        total: 0,
        presupuesto: 0,
        nombreMaxLength: 15,
        nombreMinLength: 3
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre : null,
          descripcion: null,
          importe: null,
        }
      },
      actualizar(){
        console.log(this.formData.importe)
        return this.total += parseInt(this.formData.importe)
      },
      enviar() {
        let gasto = {...this.formData}
        gasto.fecha = new Date().toLocaleString()

        console.log(gasto)
        this.gastos.push(gasto)

        this.formData = this.getInitialData()
        this.formstate._reset()
      },
      analizarSaldo() 
      {
        let color = '#000000'
        let dif = this.presupuesto - this.total
        
        console.log("pres: " + this.presupuesto + " total: " + this.total)
        if(this.presupuesto > 0 && dif < 0) color = '#ff0000'
        else if(this.total < 1000) color = '#6e931d'
        else if(this.total >= 1000 && this.total < 5000) color = '#a234d1'
        else if (this.total >= 5000) color = '#ffaa00'
        return color
      }
    },
    computed: {
    }
}


</script>

<style scoped lang="css">
  .src-componentes-ingreso {

  }

  .jumbotron {
    background-color: #f2f4ff;
    color: #4864e6;
  }

  hr {
    background-color: white;
  }

  pre {
    color: white;
  }
</style>
