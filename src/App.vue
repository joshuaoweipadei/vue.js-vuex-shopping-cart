<template>
<div id="app">
    <NarBar/>
    <router-view />
</div>
</template>

<script>
import NarBar from './components/NavBar.vue'

export default {
  components: {
    NarBar
  }
}
</script>
