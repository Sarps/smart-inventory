<template>
  <v-card class="d-flex flex-column logo d-flex justify-center" flat color="blue lighten-5" width="100%" height="100%">
    <v-spacer>
      <v-container fluid>
        <v-row dense>
          <v-col class="inventory-item" v-for="(card, index) in cards" :key="card.title" cols="12">
            <ProductCard :selected="selectedIndex === index" @select="selectedIndex = index" :card="card"
              @regenerate="onRegenerate(card)" @print="" />
          </v-col>
        </v-row>
      </v-container>
    </v-spacer>
    <AddProduct @save="onNewProduct" />
    <BottomNav />
  </v-card>
</template>

<script>
import VueBarcode from 'vue-barcode';
import Ean from 'ean-generator';

export default {
  name: 'IndexPage',

  components: {
    'barcode': VueBarcode
  },

  data: () => ({
    selectedIndex: 0,
    ean: new Ean(['084', '603']),
    cards: [
      {name: 'Milkshake', brand: 'Nestle Ltd', amount: 12.10, ean: '084', code: '6032792246612'},
      {name: 'Milo', brand: 'Tomatin Industries', amount: 9.10, ean: '084', code: '6032792246612'},
      {name: 'Mollowutu', brand: '', amount: 9.10, ean: '084', code: '6032792246612'},
      {name: 'Banana Jujutsu', brand: 'Neat Fufu LLC', amount: 9.10, ean: '084', code: '6032792246612'},
      {name: 'Agleton Banku', brand: 'Neat Fufu LLC', amount: 9.10, ean: '084', code: '6032792246612'},
      {name: 'Masterson Fufu', brand: 'Neat Fufu LLC', amount: 9.10, ean: '084', code: '6032792246612'},
      {name: 'Agleton Banku', brand: 'Neat Fufu LLC', amount: 9.10, ean: '084', code: '6032792246612'},
      {name: 'Masterson Fufu', brand: 'Neat Fufu LLC', amount: 9.10, ean: '084', code: '6032792246612'},
    ],
  }),

  methods: {
    onNewProduct({name, brand, ean, amount}) {
      const code = this.ean.create({countryCode: ean})
      console.log(code)
      this.cards.unshift({ name, brand, amount, ean, code })
      this.selectedIndex = 0;
    },
    onRegenerate(card) {
      card.code = this.ean.create({countryCode: card.ean})
    }
  }
}
</script>

<style scoped>
.inventory-item {
  transition: all 0.5s;
}
</style>
