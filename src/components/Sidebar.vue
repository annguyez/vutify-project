<template>
  <v-col 
    :class="{
        'app-left': true,
        'p-0 full-divider': !$vuetify.display.smAndDown
    }"
    cols="12"
    md="4"
    v-if="!$vuetify.display.smAndDown || !selectedApp"
  >
    <v-sheet class="pa-4" color="grey-lighten-4">
      <v-avatar class="mb-4" color="grey-darken-1" size="64"></v-avatar>
      <div>john@google.com</div>
    </v-sheet>

    <v-divider></v-divider>

    <v-text-field
      :model-value="modelValue"
      @update:model-value="$emit('update:modelValue', $event)"
      prepend-inner-icon="mdi-magnify"
      label="Search applications"
      dense
      clearable
      hide-details
      variant="outlined"
      class="ma-2"
      @click:clear="emit('update:modelValue', '')"
    />

    <v-chip class="ma-2" color="primary" variant="outlined">
      {{ filteredApps.length }} apps
    </v-chip>

    <v-list>
      <v-list-item
        v-for="app in filteredApps"
        :key="app.id"
        @click="$emit('select-app', app)"
        :class="{ 'bg-grey-lighten-3': selectedApp?.id === app.id }"
      >
        <v-list-item-title>{{ app.name }}</v-list-item-title>
      </v-list-item>
    </v-list>
  </v-col>
</template>

<script setup>
defineProps({
  filteredApps: Array,
  selectedApp: Object,
  modelValue: String
}) 

const emit = defineEmits(["update:modelValue", "select-app"])

</script>

<style scoped>
.app-left {
  height: 100vh;
  padding: 0;
}
.bg-grey-lighten-3 {
  background-color: #f5f5f5;
}

.full-divider {
border-right: 1px solid #d5d5d5;
}
</style>
