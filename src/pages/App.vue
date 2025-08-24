<template>
  <v-app id="inspire">
    <v-main>
      <v-container fluid>
        <div class="d-flex h-100 vh-100">
          <v-row>
            <!-- Sidebar -->
            <Sidebar
              v-model="searchQuery" 
              :filtered-apps="filteredApps"
              :selected-app="selectedApp"
              @select-app="selectApp"
            />

            <!-- Divider -->
            <!-- <v-divider
              v-if="!$vuetify.display.smAndDown"
              vertical
              class="mx-2 full-divider"
            /> -->

            <!-- Details -->

            <!-- <DetailContent
              :selected-app="selectedApp"
              @back="selectedApp = null"
            /> -->
            <AppDetails
              :selected-app="selectedApp"
              @back="selectedApp = null"
            />
          </v-row>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import Sidebar from "./../components/Sidebar.vue"
import AppDetails from "./../components/AppDetails.vue";

const searchQuery = ref("");
const selectedApp = ref(null);

console.log('searchQuery', searchQuery);


const apps = ref([
  {
    id: 1,
    name: "DesignBuddy",
    description: "Your design companion app.",
    access: ["View profile", "Edit projects", "Share designs"],
  },
  {
    id: 2,
    name: "TaskMaster",
    description: "Manage and track tasks.",
    access: ["Create tasks", "Update status", "View history"],
  },
  {
    id: 3,
    name: "DataVault",
    description: "Secure data storage solution.",
    access: ["Encrypt files", "Download backups", "Share securely"],
  },
]);


const filteredApps = computed(() =>
  apps.value.filter((app) =>
    app.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
);

function selectApp(app) {
  selectedApp.value = app;
}

console.log('filteredApps', filteredApps);


onMounted(() => {
  if (!selectedApp.value && filteredApps.value.length > 0) {
    selectedApp.value = filteredApps.value[0];
  }
});
</script>

<style scoped>
/* .full-divider {
  position: relative;
  right: 20px;
} */
::v-deep(.v-main) {
  overflow: hidden !important;
}
</style>
