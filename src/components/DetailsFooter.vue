<template>
  <v-sheet
    class="detail-footer"
    elevation="2"
  >
    <v-btn
      color="error"
      variant="outlined"
      prepend-icon="mdi-delete"
      @click="$emit('deleteAll')"
    >
      Delete all connections
    </v-btn>
  </v-sheet>
</template>

<script setup>
defineEmits(["deleteAll"])
</script>

<style scoped>
.detail-footer {
  position: fixed;
  bottom: 60px;
  padding: 16px;
  background-color: white;
  border-top: 1px solid #eee;
  width: -webkit-fill-available;
  display: flex;
  justify-content: flex-end;
}
</style>
