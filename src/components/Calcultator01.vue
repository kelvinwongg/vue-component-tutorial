<template>
  <div>
    <h1>Discount Calculator</h1>
    <label>Price:</label>
    <input
      :value="priceCurrency"
      @input="$emit('update:price', getNumber($event.target.value))"
      @blur="onBlur('price', $event.target.value)"
    />
    <br>
    <label>Rate:</label>
    <input
      :value="rateCurrency"
      @input="$emit('update:rate', getNumber($event.target.value))"
      @blur="onBlur('rate', $event.target.value)"
      :haha="price"
    />
    <br>
    <label>Discount:</label>
    <input
      :value="discountCurrency"
      @input="$emit('update:discount', getNumber($event.target.value))"
      @blur="onBlur('discount', $event.target.value)"
    />
  </div>
</template>

<script>
import numeral from 'numeral'

export default {
  props: [
    'price',
    'rate',
    'discount'
  ],
  data() {
    return {
      priceCurrency: this.getCurrency(this.price),
      rateCurrency: this.getCurrency(this.rate),
      discountCurrency: this.getCurrency(this.discount),
      flag: '',
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
    onBlur(input, number) {
      this[input+'Currency'] = this.getCurrency(number)
      this.$forceUpdate()
    }
  },
  watch: {
    price(newPrice) {
      if (this.flag !== 'price') {
        // Calculate discount
        console.log('Calculate discount')
        let newDiscount = this.getNumber(newPrice * this.rate / 100)
        this.$emit('update:discount', newDiscount)
        this.discountCurrency = this.getCurrency(newDiscount)
        this.priceCurrency = newPrice
        this.flag = 'discount'
      }
    },
    rate(newRate) {
      if (this.flag != 'rate') {
        // Calculate discount
        console.log('Calculate discount')
        let newDiscount = this.getNumber(this.price * newRate / 100)
        this.$emit('update:discount', newDiscount)
        this.discountCurrency = this.getCurrency(newDiscount)
        this.rateCurrency = newRate
        this.flag = 'discount'
      } else {
        this.flag = ''
      }
    },
    discount(newDiscount) {
      if (this.flag != 'discount') {
        // Calculate rate
        console.log('Calculate rate')
        let newRate = this.getNumber(newDiscount / this.price * 100)
        this.$emit('update:rate', newRate)
        this.rateCurrency = this.getCurrency(newRate)
        this.discountCurrency = newDiscount
        this.flag = 'rate'
      } else {
        this.flag = ''
      }
    },
  },
  beforeUpdate() { console.log('beforeUpdate') },
  updated() { console.log('updated') }
}
</script>