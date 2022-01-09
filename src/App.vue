<template>
  <center><div id="app">
    <header>
      <center><div class="title display-6 m-4">{{title}}</div></center>
    </header>

    <section class="main-content w-50 mx-auto">
      <ul class="nav nav-pills">
        <li
          v-for="tab in tabs"
          v-bind:key="tab"
          v-bind:href="['#', {tab}]"
          v-bind:class="['nav-link', { active: currentTab === tab }]"
          data-toggle="pill"
          v-on:click="currentTab = tab"
        >
        {{tab}}
        </li>
      </ul>
      <component v-bind:is="currentTabComponent" class="tab"></component>
    </section>
  </div></center>
</template>

<script>

import WindowsList from './components/WindowsList.vue';
import RoomsList from './components/RoomsList.vue';
import BuildingsList from './components/BuildingsList.vue';
import ContactList from './components/ContactList.vue';
import CreateList from './components/CreateList.vue'
import HeatersList from './components/HeatersList';

export default {
  name: 'App',
  components: {
    WindowsList,
    RoomsList,
    BuildingsList,
    ContactList,
    CreateList,
    HeatersList
  },
  data() {
    return {
      title: 'Faircorp',
      currentTab: "Buildings",
      tabs: ["Buildings", "Rooms", "Windows", "Heaters", "Create", "Contact"]
    }
  },
  computed: {
          currentTabComponent(){
            return this.currentTab.toLowerCase() + "-list";
          }
        }
}
</script>

<style>
  @import './assets/style2.css';
</style>
