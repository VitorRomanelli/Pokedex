<template>
  <div class="pokemon">
    <h1>{{ number }} {{ name }}</h1>
    <span>{{ url }}</span>
  </div>
</template>

<script>
export default {
  name: 'Pokemon',
  props: {
    number: Number,
    name: String,
    url: String
  }
}
</script>

<style>

</style>