<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{todaysDate}}</div>
      </div>
      <q-img src="statics/nice.jpg" class="header-image absolute-top"></q-img>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above :width="250" :breakpoint="800">
      <q-scroll-area
        style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #ddd"
      >
        <q-list padding>
          <q-item clickable v-ripple exact to="/">
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section>Todo</q-item-section>
          </q-item>

          <q-item clickable v-ripple exact to="/help">
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section>Help</q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top" src="statics/nice.jpg" style="height: 192px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
          </q-avatar>
          <div class="text-weight-bold">João Henrique Camargo</div>
          <div>@joaohhenriq</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <!--Preserve all information in a page even if when change the pages-->
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

export default {
  name: 'MainLayout',
  computed: {
    todaysDate() {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  },
  data() {
    return {
      leftDrawerOpen: false,
    }
  }
}
</script>

<style>
.header-image {
  height: 100%;
  opacity: 0.2;
  z-index: -1;
  filter: grayscale(100%);
}
</style>