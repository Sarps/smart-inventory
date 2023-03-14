<template>
  <v-card :flat="!selected" color="white" class="inventory-item"
          @click="$emit('select')" :ripple="false">
    <v-col cols="12" class="d-flex justify-center" v-if="selected">
      <barcode :value="card.code" format="EAN13">
        Show this if the rendering fails.
      </barcode>
    </v-col>
    <v-card-text class="pa-0">
      <v-list-item two-line>
        <v-list-item-content>
          <v-list-item-title v-text="card.name" />
          <v-list-item-subtitle v-text="card.brand" />
        </v-list-item-content>
        <v-list-item-action>
          <v-list-item-action-text>€ {{ card.amount }}</v-list-item-action-text>
        </v-list-item-action>
      </v-list-item>
    </v-card-text>
    <v-card-actions v-if="selected">
      <PrintDialog :product="card"/>
      <v-dialog v-model="regenerateDialog" width="500" persistent>
        <template v-slot:activator="{ on, attrs }">
          <v-btn dark depressed color="red lighten-3" class="text-none" v-on="on" v-bind="attrs">
            <v-icon left small>mdi-radar</v-icon>
            Change Code
          </v-btn>
        </template>

        <v-card>
          <v-card-title class="subtitle-1 grey lighten-2">Regenerate Code</v-card-title>
          <v-card-text class="mt-3">Changing code will delete the old one forever!</v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="red" text @click="regenerateDialog = false">Cancel</v-btn>
            <v-btn color="primary" text @click="onRegenerate">Proceed</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-card-actions>
  </v-card>
</template>

<script>
import barcode from "vue-barcode";

export default {
  name: "ProductCard",
  components: {barcode},
  props: ['selected', 'card'],
  data: () => ({
    regenerateDialog: false
  }),
  methods: {
    onRegenerate() {
      this.$emit('regenerate')
      this.regenerateDialog = false
    }
  }
}
</script>

<style scoped>

</style>
