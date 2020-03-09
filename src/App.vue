<template>
  <v-app>
    <NavBar />
    <v-content>
      <MemoryTest/>
    </v-content>
    <v-footer padless>
      <v-col
          class="text-center"
          cols="12"
      >
        {{ new Date().getFullYear() }} — <strong>Tom Caiger</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
import MemoryTest from './components/MemoryTest';
import NavBar from './components/NavBar';

export default {
  name: 'App',
  components: {
    MemoryTest,
    NavBar,
  },
};
</script>
