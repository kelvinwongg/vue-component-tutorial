<template>
  <div>
    <calculator
      :price="parentPrice"
      :rate="parentRate"
      :discount="parentDiscount"
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
