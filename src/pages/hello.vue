<template>
  <v-app>
    <!-- Mobile: header -->
    <v-app-bar v-if="$vuetify.display.smAndDown" color="white" flat>
      <v-container class="d-flex align-center bg-grey-lighten-3">
        <v-img
          src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/Viettel_logo_2021.svg/2560px-Viettel_logo_2021.svg.png"
          max-width="90"
          contain
        />
        <div class="ml-3">
          <div class="text-subtitle-1 font-weight-bold">Viettel AFS</div>
          <div class="text-caption">Viettel Anti-fraud Service</div>
        </div>
      </v-container>
    </v-app-bar>

    <!-- Mobile: full screen form -->
    <v-main v-if="$vuetify.display.smAndDown">
      <v-container class="d-flex align-center justify-center">
        <v-col cols="12">
          <LoginForm />
        </v-col>
      </v-container>
    </v-main>

    <!-- Desktop: dialog -->
    <v-main v-else>
      <v-container class="fill-height d-flex align-center justify-center">
        <!-- <v-dialog v-model="open" persistent max-width="420" open-on-mount> -->
          <v-card class="pa-6">
            <LoginForm />
          </v-card>
        <!-- </v-dialog> -->
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import LoginForm from '@/components/LoginForm.vue';
import { ref } from 'vue'

const open = ref(true)
</script>
