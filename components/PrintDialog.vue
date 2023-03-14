<template>
  <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
    <template v-slot:activator="{ on, attrs }">
      <v-btn dark color="primary" class="text-none mr-3" v-bind="attrs" v-on="on">
        <v-icon left small>mdi-printer-3d</v-icon>
        Print
      </v-btn>
    </template>
    <v-card>
      <v-toolbar dark color="primary">
        <v-btn icon dark @click="dialog = false">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-toolbar-title>Print Form</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items>
          <v-btn dark text v-print="'#printMe'">
            Proceed
          </v-btn>
        </v-toolbar-items>
      </v-toolbar>
      <v-divider></v-divider>
      <v-subheader>Details</v-subheader>
      <v-card-text class="pa-0 px-2">
        <v-container>
          <v-row>
            <v-col cols="4" class="py-0">
              <v-text-field label="Width" prepend-inner-icon="mdi-tape-measure"
                            v-model="width" required/>
            </v-col>
            <v-col cols="4" class="py-0">
              <v-text-field label="Height" prepend-inner-icon="mdi-tape-measure"
                            v-model="height" required/>
            </v-col>
            <v-col cols="4" class="py-0">
              <v-select label="Sheet" prepend-inner-icon="mdi-tape-measure" return-object
                        v-model="sheet" :items="sheets" item-text="name" required/>
            </v-col>
            <v-col cols="12">
              <v-divider />
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <PrintScreen v-if="sheet" :cols="cols" :rows="rows" :height="sheet.height" :width="sheet.width" :code="product.code" />
      <v-card-text>
        <v-img v-if="sheet" :aspect-ratio="sheet.width/sheet.height" class="grey lighten-3" width="100%">
          <v-sheet min-height="100%" height="100%" class="fill-height d-flex flex-column justify-space-between" color="transparent">
            <v-sheet width="100%" v-for="i in rows" :key="i"
                     class="fill-height d-flex flex-row justify-space-between" color="transparent">
                <v-spacer outlined v-for="j in cols" :key="`${i}${j}`" color="red">
                  <v-img :aspect-ratio="width/height" class="grey lighten-4 pa-1">
                    <v-sheet color="grey lighten-5" width="100%" min-height="100%" />
                  </v-img>
                </v-spacer>
            </v-sheet>
          </v-sheet>
        </v-img>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "PrintDialog",
  props: ['product'],
  data() {
    return {
      dialog:  false,
      width:   5,
      height:  2,
      sheet:   null,
      cols: 1,
      rows: 1,
      sheets:  [
        {
          name: "Legal", width: 21.6, height: 35.6
        },
        {
          name: "Tabloid", width: 27.9, height: 43.2
        },
        {
          name: "Letter", width: 21.6, height: 27.9
        },
        {
          name: "A0", width: 84.1, height: 118.9
        },
        {
          name: "A1", width: 59.4, height: 84.1
        },
        {
          name: "A2", width: 42.0, height: 59.4
        },
        {
          name: "A3", width: 29.7, height: 42.0
        },
        {
          name: "A4", width: 21.0, height: 29.7
        },
        {
          name: "A5", width: 14.8, height: 21.0
        },
      ]
    }
  },
  mounted() {
    this.sheet = this.sheets[7]
    this.updateDimensions();
  },
  methods: {
    onPrint() {
      this.dialog = false;
    },
    updateDimensions() {
      this.cols = Math.floor(this.sheet.width / this.width)
      this.rows = Math.floor(this.sheet.height / this.height)
    }
  }
}
</script>

<style scoped>

</style>
