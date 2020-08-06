<template>
  <div>
    <calculator
      :price="parentPrice"
      @update:price="parentPrice = $event"
      :rate="parentRate"
      @update:rate="parentRate = $event"
      :discount="parentDiscount"
      @update:discount="parentDiscount = $event"
    />
  </div>
</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'App',
  components: {
    Calculator,
  },
  data: () => ({
    parentPrice: 200,
    parentRate: 90,
    parentDiscount: 180,
  }),
};
</script>
