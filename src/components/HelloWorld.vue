<template>
  <v-container fluid>
    <v-layout row wrap>
      <v-flex xs12>
        <h1>Lista de Propiedades</h1>
      </v-flex>
      <v-flex xs4>
        <v-btn @click="dialog = true" dark color="green">
          Agregar Propiedad
        </v-btn>
      </v-flex>
    </v-layout>
    <v-layout row wrap>
      <v-flex xs12 md6>
        <v-card dark color="red" v-for="propiedad in propiedades" :key="propiedad.id">
        <v-card-title primary-title>
          <div>
            <h3 class="headline mb-0">{{ propiedad.nombre }}</h3>
            <div>{{ propiedad.descripcion }}</div>
          </div>
        </v-card-title>
        <v-card-actions>
          <v-btn color="blue" @click="verPropiedad(propiedad)">Ver</v-btn>
          <v-btn color="blue" @click="editarPropiedad(propiedad)">Editar</v-btn>
        </v-card-actions>
      </v-card>
      </v-flex>
    </v-layout>
    <propiedad-form @nuevaPropiedad="nuevaPropiedad" @closeDialog="dialog = false" :dialog="dialog"></propiedad-form>
  </v-container>
</template>

<script>
import {propiedadService} from '@/services/Propiedad.service'
import PropiedadForm from '@/components/PropiedadForm'
export default {
  data () {
    return {
      propiedades: [],
      dialog: false
    }
  },
  mounted () {
    let vm = this
    propiedadService.query().then(data => {
      vm.propiedades = data.body
    }, erro => {
      console.log('error')
    })
  },
  methods: {
    nuevaPropiedad (propiedad) {
      let vm = this
      vm.propiedades.push(propiedad)
    },
    editarPropiedad (propiedad) {
      let vm = this
      vm.dialog = true
      vm.$emit('editar', propiedad)
    },
    verPropiedad (propiedad) {
      let vm = this
      vm.dialog = true
      vm.$emit('ver', propiedad)
    }
  },
  components: {PropiedadForm}
}
</script>




