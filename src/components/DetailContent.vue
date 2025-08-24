<template>
  <div class="content" v-if="selectedApp">
    <h2>{{ selectedApp.name }}</h2>
    <p>{{ selectedApp.description }}</p>

    <v-divider class="my-4" />

    <h3>Access Given</h3>
    <ul>
      <li v-for="(item, i) in selectedApp.access" :key="i">
        {{ item }}
      </li>
    </ul>
  </div>
  <div v-else>
    <p>Select an app to view details</p>
  </div>
</template>

<script setup>
defineProps({
  selectedApp: Object
})
</script>
<style scoped>
.content {
  padding: 32px;
}
</style>
