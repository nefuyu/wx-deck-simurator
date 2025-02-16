<template>
  <ul class="tabs">
    <li v-for="tab in tabs" :key="tab.id" :class="{select: currentTab === tab.id}" class="tab"
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
        {id: 1, title: "Edit"},
        {id: 2, title: "View"}
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

.tabs {
  border-bottom: 1px solid black;
}

.tab {
  display: inline-block;
  border-top: 1px solid black;
  border-left: 1px solid black;
  border-right: 1px solid black;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  padding-top: 15px;
  padding-bottom: 5px;
  padding-left: 30px;
  padding-right: 30px;
  cursor: pointer;
}

.tab.select {
  background-color: aquamarine;
}
</style>
