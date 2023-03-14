<template>
  <v-app dark>
    <v-app-bar fixed app extended extension-height="80" height="80"
               color="primary" dark class="rounded-b-xl">
      <v-list-item two-line>
        <v-list-item-content>
          <v-list-item-title class="font-weight-medium overline">Kumasi Market</v-list-item-title>
          <v-list-item-subtitle class="font-weight-bold headline">Inventory</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-spacer/>
      <v-btn icon>
        <v-icon>mdi-cog-outline</v-icon>
      </v-btn>
      <template #extension>
        <v-text-field prepend-inner-icon="mdi-magnify" label="Search for Products" flat
                      rounded solo-inverted class="mt-2"/>
      </template>
    </v-app-bar>
    <v-main>
      <v-container class="fill-height pa-0">
        <Nuxt/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      title: 'Inventory'
    }
  }
}
</script>
