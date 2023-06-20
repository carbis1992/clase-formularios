<template>
  <div>
    <formulario-component @datosIngresados="agregarDato" />
    <tabla-component :data="datos" />
  </div>
</template>

<script>
import FormularioComponent from './components/FormularioComponent.vue';
import TablaComponent from './components/TablaComponent.vue';

export default {
  components: {
    FormularioComponent,
    TablaComponent
  },
  data() {
    return {
      datos: []
    };
  },
  methods: {
    agregarDato(dato) {
      this.datos.push(dato);
    }
  }
};
</script>
