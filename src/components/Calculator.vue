<template>
  <div>
    <h1>Calculator</h1>
    <label>Price:</label>
    <input
      :value="price"
    />
    <br>
    <label>Rate:</label>
    <input
      :value="rate"
    />
    <br>
    <label>Discount:</label>
    <input
      :value="discount"
    />
  </div>
</template>

<script>
export default {
  props: ['price', 'rate', 'discount'],
}
</script>

<style>

</style>