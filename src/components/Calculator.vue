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
export default {
  props: ['price', 'rate', 'discount'],
}
</script>

<style>

</style>