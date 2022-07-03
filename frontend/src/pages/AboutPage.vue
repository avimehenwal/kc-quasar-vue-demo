<template>
  <q-page padding>
    <!-- content -->
    <h2>About Page</h2>
    <router-link to="/">
      <p>Back to home</p>
    </router-link>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'AboutPage'
})
</script>
