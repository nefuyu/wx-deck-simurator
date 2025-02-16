<template>
  <ul class="">
    <li v-for="tab in tabs" :key="tab.id" :class="{select: currentTab === tab.id}" class=""
      @click="selected(tab.id)">
      {{ tab.title }}
    </li>
  </ul>
  <EditMode v-if="currentTab === 1" :lrigCards="lrigCards" :mainCards="mainCards"/>
  <ViewMode v-if="currentTab === 2" :lrigCards="lrigCards" :mainCards="mainCards"/>
</template>

<script>
import EditMode from './components/EditMode.vue'
import ViewMode from './components/ViewMode.vue'

export default {
  name: 'App',
  components: {
    EditMode,
    ViewMode
  },
  data() {
    return {
      lrigCards: [],
      mainCards: [],
      currentTab: 1,
      tabs: [
        {id: 1, title: "edit"},
        {id: 2, title: "view"}
      ],
    }
  },
  methods: {
    selected(id) {
      this.currentTab = id;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
