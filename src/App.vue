<script>
import Input from "@/components/Input.vue";
import Selector from "@/components/Selector.vue";

export default {
  components: {Input, Selector}
}
</script>

<template>
  <h1>Crypto</h1>
  <Input/>

  <div className="selectors">
    <Selector/>
    <Selector/>
  </div>
</template>

<style scoped>
  .selectors {
    display: flex;
    justify-content: space-around;
    width: 700px;
    margin: 0 auto;
  }
</style>
