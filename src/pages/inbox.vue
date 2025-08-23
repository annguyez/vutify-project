<template>
  <v-app id="inspire">
    <v-main>
    <v-system-bar>
      <v-spacer></v-spacer>

      <v-icon>mdi-square</v-icon>

      <v-icon>mdi-circle</v-icon>

      <v-icon>mdi-triangle</v-icon>
    </v-system-bar>

    <v-container fluid>
        <div class="d-flex h-100">
        <v-row>
          <!-- Cột trái: danh sách -->
          <v-col 
            cols="12"
            md="4"
            v-if="!$vuetify.display.smAndDown || !selectedApp"
          >
            <v-sheet
                class="pa-4"
                color="grey-lighten-4"
            >
                <v-avatar
                class="mb-4"
                color="grey-darken-1"
                size="64"
                ></v-avatar>

                <div>john@google.com</div>
            </v-sheet>

            <v-divider></v-divider>

            <v-text-field
                v-model="searchQuery"
                prepend-inner-icon="mdi-magnify"
                label="Search applications"
                dense
                hide-details
                variant="outlined"
                class="ma-2"
                />
                <v-chip class="ma-2" color="primary" variant="outlined">
  {{ filteredApps.length }} apps
</v-chip>

             <v-list>
                    <v-list-item
            v-for="app in filteredApps"
            :key="app.id"
            @click="selectApp(app)"
            :class="{ 'bg-grey-lighten-3': selectedApp?.id === app.id }"
          >
          <v-list-item-title>{{ app.name }}</v-list-item-title>
                </v-list-item>
                </v-list>
            </v-col>
        <v-divider
            v-if="!$vuetify.display.smAndDown"
            vertical
            class="mx-2 full-divider"
        ></v-divider>
  
            <v-col style="flex: 1" 
                cols="12"
                md="8"
                v-if="!$vuetify.display.smAndDown || selectedApp"
            >
                <v-btn
                v-if="$vuetify.display.smAndDown && selectedApp"
                prepend-icon="mdi-arrow-left"
                variant="text"
                @click="selectedApp = null"
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
          </v-row>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<style scoped>
html {
    overflow: hidden !important;
}
  .inbox-container {
  height: calc(100vh - 64px);
  overflow: scroll;
}

.scrollable-card {
  height: 100%;
  overflow-y: auto;
}

.h-screen {
  height: 100vh;
}
.app-left {
  width: 300px; /* fix width cột trái */
  flex-shrink: 0;
}
.app-right {
  overflow-y: auto;
}
.bg-grey-lighten-3 {
    background-color: #f5f5f5;
}

.full-divider {
    position: relative;
    right: 10px
}
</style>


<!-- <script setup>
  import { ref } from 'vue'
``
  const cards = ['Today', 'Yesterday']
  const links = [
    ['mdi-inbox-arrow-down', 'Inbox'],
    ['mdi-send', 'Send'],
    ['mdi-delete', 'Trash'],
    ['mdi-alert-octagon', 'Spam'],
  ]
const mails = ref([
  { title: "Inbox 1", content: "Nội dung thư số 1" },
  { title: "Inbox 2", content: "Nội dung thư số 2" },
  { title: "Inbox 3", content: "Nội dung thư số 3" },
]);
  const selectedMail = ref(null);

    function selectMail(mail) {
        selectedMail.value = mail;
    }

  const drawer = ref(null)
</script> --> -->


<script setup>
import { ref, computed } from "vue";

const searchQuery = ref("");
const selectedApp = ref(null);

const apps = ref([
  {
    id: 1,
    name: "DesignBuddy",
    logo: "https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png",
    description: "Your design companion app.",
    access: ["View profile", "Edit projects", "Share designs"],
  },
  {
    id: 2,
    name: "TaskMaster",
    logo: "https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png",
    description: "Manage and track tasks.",
    access: ["Create tasks", "Update status", "View history"],
  },
  {
    id: 3,
    name: "DataVault",
    logo: "https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png",
    description: "Secure data storage solution.",
    access: ["Encrypt files", "Download backups", "Share securely"],
  },
]);

// Lọc danh sách theo search
const filteredApps = computed(() =>
  apps.value.filter((app) =>
    app.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
);

function selectApp(app) {
  selectedApp.value = app;
}
</script>
<script>
  export default {
    data: () => ({
      cards: ['Today', 'Yesterday'],
      drawer: null,
      links: [
        ['mdi-inbox-arrow-down', 'Inbox'],
        ['mdi-send', 'Send'],
        ['mdi-delete', 'Trash'],
        ['mdi-alert-octagon', 'Spam'],
      ],
    }),
  }
</script>