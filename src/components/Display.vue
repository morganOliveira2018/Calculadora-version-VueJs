<template>
  <div class="display">
      {{ value }}
  </div>
</template>

<script>
export default {
  props: ['value']
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