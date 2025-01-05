<template>

  <v-layout class="overflow-visible" style="height: 56px;">
    <v-bottom-navigation
      v-model="value"
      :bg-color="color"
      mode="shift"
      style="position: fixed; bottom: 0; width: 100%; z-index: 10;"
    >
      <v-btn to="/">
        <v-icon>mdi-home</v-icon>
        <span>Inicio</span>
      </v-btn>
      <v-btn to="/destilacion">
        <v-icon>mdi-flask-round-bottom</v-icon>
        <span>Destilación</span>
      </v-btn>
      <v-btn to="/fundamentos">
        <v-icon>mdi-book-open-blank-variant</v-icon>
        <span>Fundamentos</span>
      </v-btn>
      <v-btn to="/about">
        <v-icon>mdi-information-slab-circle-outline</v-icon>
        <span>Acerca de</span>
      </v-btn>
    </v-bottom-navigation>
  </v-layout>
</template>
<script>
export default {
  data: () => ({value: 1}),

  computed: {
    color() {
      switch (this.value) {
        case 0:
          return 'blue-grey'
        case 1:
          return 'teal'
        case 2:
          return 'brown'
        case 3:
          return 'indigo'
        default:
          return 'blue-grey'
      }
    },
  },
}
</script>
