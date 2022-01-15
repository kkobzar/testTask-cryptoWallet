<template>
  <div id="app">
    <Navigation/>
    <router-view/>
  </div>
</template>

<style>
/*
Bootstrap v5 import
*/
@import "https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css";
</style>
<script>
import Navigation from "@/components/Navigation";
export default {
  components: {Navigation}
}
</script>
