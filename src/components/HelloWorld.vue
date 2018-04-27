<template>
  <v-container fluid>
    <v-layout row wrap>
      <v-flex xs12>
        <h1>Lista de Propiedades</h1>
      </v-flex>
      <v-flex xs12 md6>
        <v-card dark color="red" v-for="propiedad in propiedades" :key="propiedad.id">
        <v-card-title primary-title>
          <div>
            <h3 class="headline mb-0">{{ propiedad.nombre }}</h3>
            <div>{{ propiedad.descripcion }}</div>
          </div>
        </v-card-title>
      </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import {propiedadService} from '@/services/Propiedad.service'
export default {
  data () {
    return {
      propiedades: []
    }
  },
  mounted () {
    let vm = this
    propiedadService.query().then(data => {
      vm.propiedades = data.body
    }, erro => {
      console.log('error')
    })
  }
}
</script>




