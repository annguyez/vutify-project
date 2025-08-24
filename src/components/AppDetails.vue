<template>
  <v-col style="flex: 1" cols="12" md="8" v-if="!$vuetify.display.smAndDown || selectedApp">
    <v-btn
      v-if="$vuetify.display.smAndDown && selectedApp"
      prepend-icon="mdi-arrow-left"
      variant="text"
      @click="$emit('back')"
      class="mb-2"
    >
      Quay lại
    </v-btn>

    <div v-if="selectedApp">
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
  </v-col>
</template>

<script setup>
defineProps({
  selectedApp: Object
})

defineEmits(["back"])
</script>
