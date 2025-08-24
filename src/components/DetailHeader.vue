<template>
  <v-btn
    v-if="showBackButton"
    prepend-icon="mdi-arrow-left"
    variant="text"
    @click="$emit('back')"
    class="mb-2"
  >
    Quay lại
  </v-btn>
</template>

<script setup>
defineProps({
  showBackButton: Boolean
})
defineEmits(["back"])
</script>
