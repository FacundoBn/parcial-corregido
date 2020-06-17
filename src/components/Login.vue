<template>
  <section class="src-components-login">
     
    <div v-if="!this.log">
      <div class="jumbotron mt-3">
      <vue-form :state="formLogin" @submit.prevent="check()">

      <validate tag="div">
        <label for="user">Usuario:</label>
        <input 
          type="text"
          id="user"
          class="form-control"
          autocomplete="off"
          name="user"
          v-model.trim="formData.user"
          required
          no-espacios
          :minlength="nomMin"
          :maxlength="nomMax"
        >
        <field-messages name="user" show="$dirty">
          <!-- <div class="alert alert-success my-1">Campo correcto</div> -->
          <div slot="required" class="alert alert-danger my-1">Campo Nombre requerido</div>
          <div slot="no-espacios" class="alert alert-danger my-1">No se permiten espacios intermedios en este campo</div>
          <div slot="minlength" class="alert alert-danger my-1">Los caracteres minimos son {{nomMin}}</div>
          <div slot="maxlength" class="alert alert-danger my-1">Los caracteres maximos son {{nomMax}}</div>
          
        </field-messages>


      </validate>
      <br>

      <validate tag="div">
        <label for="password">Password</label>
        <input 
          type="password"
          id="password"
          class="form-control"
          autocomplete="off"
          name="password"
          v-model.trim="formData.password"
          required
        >
        <field-messages name="password" show="$dirty">
          <!-- <div class="alert alert-success my-1">Campo correcto</div> -->
          <div slot="required" class="alert alert-danger my-1">Campo Password requerido</div>
        </field-messages>
      </validate>
      <br>

      <button class="btn btn-success my-4" :disabled="formData.$invalid" type="submit">Log {{mensaje}}</button>

      </vue-form>
      </div>
    </div>
    <div v-else>
      <Navbar />
      <router-view></router-view>
      <button class="btn btn-warning my-4" @click="logout()">LogOut</button>
      
    </div>
    
  </section>
  
</template>

<script lang="js">

 import Navbar from './Navbar.vue'

  export default  {
    name: 'src-components-login',
    props: [],
    components: {
       Navbar,
    },
    mounted () {

    },
    data () {
      return {
        user: '',
        password: '',
        mensaje: '',
        formLogin : {},
        formData : this.getInitialData(),
        nomMin: 4,
        nomMax: 15,
        log : false
      }
    },
    methods: {
      getInitialData() {
        return {
          user: '',
          password: '',
          mensaje: '',
        }
      },
      
      check(){
        if (this.formData.user == 'root' && this.formData.password == '1234') {
          this.log = true
          this.formData = this.getInitialData()
        }else{
          this.mensaje='Password Incorrecto'
        }
      },

      logout() {
        this.log = false
        this.formData = this.getInitialData()
      }
    },
    computed: {
    }
}


</script>

<style scoped lang="css">
.jumbotron {
    background-color:steelblue;
    color: white;
}
</style>
