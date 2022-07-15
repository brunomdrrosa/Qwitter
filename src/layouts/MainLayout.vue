<template>
  <q-layout view="lHr lpR fFf">
    <q-header bordered class="bg-white text-black" height-hint="98">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="text-weight-bold"> Qwitter </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer show-if-above v-model="left" side="left" bordered :width="283">
      <q-icon class="q-pa-md" name="fas fa-dove" size="lg" color="primary" />

      <q-list>
        <q-item to="/" clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="home" size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold">Página Inicial</q-item-section>
        </q-item>
        <q-item to="/sobre" clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="help" size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold">Sobre</q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <!-- drawer content -->
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const rightDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },

      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value;
      },
    };
  },
};
</script>
