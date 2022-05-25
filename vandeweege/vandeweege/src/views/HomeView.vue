<template>
  <div style="padding-left: 5rem">
    <Curtains msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Curtains from "@/components/Curtains.vue"; // @ is an alias to /src

@Component({
  components: {
    Curtains,
  },
})
export default class HomeView extends Vue {}
</script>
