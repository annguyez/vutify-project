<!-- <template>
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
</script> -->
<template>
  <v-col class="detail-content" style="flex: 1" cols="12" md="8" v-if="!$vuetify.display.smAndDown || selectedApp">
    <AppDetailHeader 
      v-if="$vuetify.display.smAndDown && selectedApp" 
      @back="$emit('back')" 
      :showBackButton="true"
    />

    <AppDetailContent :selectedApp="selectedApp" />

    <AppDetailFooter @deleteAll="onDeleteAll" />
  </v-col>
</template>

<script setup>
import AppDetailHeader from './DetailHeader.vue'
import AppDetailContent from './DetailContent.vue'
import AppDetailFooter from './DetailsFooter.vue'

function onDeleteAll() {
  console.log("Delete all clicked")
}

defineProps({
  selectedApp: Object
})
defineEmits(["back"])
</script>
<style scoped>
.detail-content {
  padding: 0px;
}
</style>