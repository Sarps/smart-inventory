<template>
  <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
    <template v-slot:activator="{ on, attrs }">
      <v-btn elevation="12" fab color="primary" v-bind="attrs" v-on="on" bottom right fixed style="z-index: 100">
        <v-icon>mdi-package-variant-closed-plus</v-icon>
      </v-btn>
    </template>
    <v-card>
      <v-toolbar dark color="primary">
        <v-btn icon dark @click="dialog = false">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-toolbar-title>New Product</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items>
          <v-btn dark text @click="onSave">
            Save
          </v-btn>
        </v-toolbar-items>
      </v-toolbar>
      <v-list three-line subheader>
        <v-subheader>Notice</v-subheader>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title>Code generation</v-list-item-title>
            <v-list-item-subtitle>Generated bar codes may conflict with codes in the shop. Scan generated bar codes to
              be sure it doesn't already exist
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-subheader>Details</v-subheader>
      <v-card-text class="pa-0 px-2">
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4" class="py-0">
              <v-text-field label="Product Name" prepend-inner-icon="mdi-shopping"
                            v-model="name" required/>
            </v-col>
            <v-col cols="12" sm="6" md="4" class="py-0">
              <v-text-field label="Price" prepend-inner-icon="mdi-shopping"
                            v-model="amount" required/>
            </v-col>
            <v-col cols="12" sm="6" md="4" class="py-0">
              <v-text-field label="Brand / Manufacturer" hint="Optional manufacturer's name"
                            prepend-icon="mdi-watermark" v-model="brand"/>
            </v-col>
            <v-col cols="12" sm="6" md="4" class="py-0">
              <v-select label="Origin Country" hint="Optional"
                        item-text="name" item-value="ean" v-model="ean"
                        prepend-icon="mdi-flag-checkered" :items="countries"/>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "AddProduct",
  data() {
    return {
      dialog:    false,
      name:      '',
      amount:     '',
      brand:     '',
      ean:       '084',
      widgets:   false,
      countries: [
        {name: "Ghana", ean: "084"},
        {name: "Spain", ean: "603"},
      ]
    }
  },
  methods: {
    onSave() {
      this.$emit('save', {name: this.name, brand: this.brand, ean: this.ean, amount: this.amount})
      this.dialog = false;
    },
    onChangeCode() {

    }
  }
}
</script>

<style scoped>

</style>
