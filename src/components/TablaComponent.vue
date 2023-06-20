<template>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Nombre</th>
          <th scope="col">Email</th>
          <th scope="col">Teléfono</th>
          <th scope="col">Fecha de nacimiento</th>
          <th scope="col">País de residencia</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in data" :key="index" scope="row">
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.phone }}</td>
          <td>{{ item.birthDate }}</td>
          <td>{{ item.country }}</td>
        </tr>
      </tbody>
    </table>
</template>

<script>
export default {
  name: "TablaComponent",
  props: {
    data: {
      type: Array,
      default: () => []
    }
  }
};
</script>
