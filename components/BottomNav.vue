<template>
  <v-bottom-navigation fixed shift class="rounded-t-xl" v-model="nav">
    <v-btn>
      <span>Home</span>
      <v-icon>mdi-home-roof</v-icon>
    </v-btn>
    <v-btn>
      <span>Stock</span>
      <v-icon>mdi-family-tree</v-icon>
    </v-btn>
    <v-btn>
      <span>Prints</span>
      <v-icon>mdi-calendar-month-outline</v-icon>
    </v-btn>
  </v-bottom-navigation>
</template>

<script>
export default {
  name: "BottomNav",
  data: () => ({
    nav: 1
  })
}
</script>

<style scoped>

</style>
