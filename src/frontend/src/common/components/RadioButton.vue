<template>
  <label class="radio ingredients__input">
    <input type="radio" name="sauce" :value="value" />
    <span>{{ name }}</span>
  </label>
</template>

<script>
export default {
  name: "RadioButton",
};
</script>
