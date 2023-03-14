<template>
  <table id="printMe">
    <tbody>
    <tr v-for="i in rows" :key="i" class="red">
      <td v-for="j in cols" :key="`${i}${j}`">
        <barcode :value="code" format="EAN13" class="d-inline-block">
          Show this if the rendering fails.
        </barcode>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>
import barcode from "vue-barcode";

export default {
  name:       "PrintScreen",
  components: {barcode},
  props:      ['rows', 'cols', 'width', 'height', 'code']
}
</script>

<style scoped>
#printMe {
  display: none;
}

@media print {
  #printMe {
    display: block;
  }
}
</style>
