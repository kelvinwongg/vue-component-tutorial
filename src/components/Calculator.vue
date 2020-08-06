<template>
  <div>
    <h1>Calculator</h1>
    <label>Price:</label>
    <input
      :value="price"
      @change="$emit('update:price', $event.target.value)"
    />
    <br>
    <label>Rate:</label>
    <input
      :value="rate"
      @change="$emit('update:rate', $event.target.value)"
    />
    <br>
    <label>Discount:</label>
    <input
      :value="discount"
      @change="$emit('update:target', $event.target.value)"
    />
  </div>
</template>

<script>
import numeral from 'numeral'

export default {
  props: ['price', 'rate', 'discount'],
  methods: {
    getNumber(string) {
      const numberString = numeral(string).format('0,0.00')
      return numeral(numberString).value()
    },
    getCurrency(number) {
      return numeral(number).format('0,0.00')
    },
  }
}
</script>

<style>

</style>