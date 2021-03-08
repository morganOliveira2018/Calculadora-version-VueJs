<template>
  <div class="display">
      {{ value | size }}
  </div>
</template>

<script>
export default {
  props: ['value'],
  filters: {
    size: function(valor) {
      valor = parseFloat(valor).toFixed(2);
      return `${valor}`
    }
  }
}
</script>

<style>

.display {
  grid-column: span 4;
  background-color: black;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 10px;
  font-size: 3em;
  overflow: hidden;

}

</style>