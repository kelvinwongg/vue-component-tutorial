<template>
  <div style="margin-left: 50px;">
    <h1>Discount Calculator</h1>
    <label>Price:</label>
    <input
      :value="priceDisplay"
      @change="onChange('price', $event)"
    />
    <br>
    <label>Rate:</label>
    <input
      :value="rateDisplay"
      @change="onChange('rate', $event)"
    />
    <br>
    <label>Discount:</label>
    <input
      :value="discountDisplay"
      @change="onChange('discount', $event)"
    />
  </div>
</template>

<script>
import numeral from 'numeral'

export default {
  props: ['price', 'rate', 'discount'],
  data() {
    return {
      flag: '',
      priceDisplay: this.getCurrency(this.price),
      priceNumber: this.getNumber(this.price),
      rateDisplay: this.getCurrency(this.rate),
      rateNumber: this.getNumber(this.rate),
      discountDisplay: this.getCurrency(this.discount),
      discountNumber: this.getNumber(this.discount),
    }
  },
  watch: {
    priceNumber(newPrice) {
      if (this.flag != 'price') {
        // calculate discountNumber
        let newDiscount = this.getNumber(newPrice * this.rateNumber / 100)
        this.discountNumber = newDiscount
        
        // update currency display
        this.discountDisplay = this.getCurrency(newDiscount)

        // emit change
        this.$emit('update:discount', newDiscount)

        this.flag = 'discount'
      } else {
        this.flag = ''
      }
    },
    rateNumber(newRate) {
      if (this.flag != 'rate') {
        // calculate discountNumber
        let newDiscount = this.getNumber(this.priceNumber * newRate / 100)
        this.discountNumber = newDiscount
        
        // update currency display
        this.discountDisplay = this.getCurrency(newDiscount)

        // emit change
        this.$emit('update:discount', newDiscount)

        this.flag = 'discount'
      } else {
        this.flag = ''
      }
    },
    discountNumber(newDiscount) {
      if (this.flag != 'discount') {
        // calculate rateNumber
        let newRate = this.getNumber(newDiscount / this.priceNumber * 100)
        this.rateNumber = newRate

        // update currency display
        this.rateDisplay = this.getCurrency(newRate)

        // emit change
        this.$emit('update:rate', newRate)

        this.flag = 'rate'
      } else {
        this.flag = ''
      }
    }
  },
  methods: {
    getNumber(string) {
      const numberString = numeral(string).format('0,0.00')
      return numeral(numberString).value()
    },
    getCurrency(number) {
      return numeral(number).format('0,0.00')
    },
    onChange(input, event) {
      const inputValue = event.target.value
      this[input+'Number'] = this.getNumber(inputValue)
      this[input+'Display'] = this.getCurrency(inputValue)
      this.$emit('update:'+input, this.getNumber(inputValue))
      this.$forceUpdate()
    }
  }
}
</script>

<style>

</style>