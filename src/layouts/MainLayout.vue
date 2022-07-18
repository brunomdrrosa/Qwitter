<template>
  <q-layout view="lHr lpR fFf">
    <q-header bordered class="bg-white text-black">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="left = !left" />

        <q-toolbar-title class="text-weight-bold">
          <span class="gt-sm">{{ $route.name }}</span>
          <q-icon
            class="header-icon q-pa-md lt-md"
            name="fas fa-dove"
            size="sm"
            color="primary"
          />
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer show-if-above v-model="left" side="left" bordered :width="283">
      <q-icon class="q-pa-md" name="fas fa-dove" size="lg" color="primary" />
      <q-list>
        <q-item to="/" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="home" size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold">Página Inicial</q-item-section>
        </q-item>
        <q-item to="/sobre" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="help" size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold"
            >Sobre</q-item-section
          >
        </q-item>
      </q-list>
    </q-drawer>

    <q-drawer show-if-above v-model="right" side="right" bordered>
      <q-input placeholder="Buscar no Qwitter" outlined rounded class="q-ma-md">
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>
      <q-list padding separator>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">Futebol</q-item-label>
            <q-item-label class="text-weight-bold">Lewa</q-item-label>
            <q-item-label caption
              >Fim da novela! Lewandowski fecha com o Barcelona por 50 milhões
              de euros.</q-item-label
            >
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>há 3 minutos</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey"
              >UEFA Champions League</q-item-label
            >
            <q-item-label class="text-weight-bold">Barça</q-item-label>
            <q-item-label caption
              >Barcelona e Bayern se aproximam de acordo por
              Lewandowski.</q-item-label
            >
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>há 30 minutos</q-item-label>
          </q-item-section>
        </q-item>

        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">Futebol</q-item-label>
            <q-item-label class="text-weight-bold">Oscar</q-item-label>
            <q-item-label caption
              >Flamengo abriu negociações com o meia Oscar, do Shangai
              SIPG.</q-item-label
            >
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>há 23 minutos</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>

  </q-layout>
</template>

<script>
export default {
  data () {
    return {
      left: false,
      right: false
    }
  }
}
</script>

<style lang="sass">
.header-icon
  position: absolute
  bottom: 0
  left: 50%
  transform: translateX(-50%)
</style>
