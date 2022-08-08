<template>
  <div class="content__pizza">
    <label class="input">
      <span class="visually-hidden">Название пиццы</span>
      <input
        type="text"
        name="pizza_name"
        placeholder="Введите название пиццы"
        :value="pizzaName"
        @input="setName"
      />
    </label>

    <builder-pizza-view />

    <builder-price-counter />
  </div>
</template>

<script>
import BuilderPizzaView from "@/modules/builder/BuilderPizzaView";
import BuilderPriceCounter from "@/modules/builder/BuilderPriceCounter";
export default {
  name: "BuilderContentPizza",
  components: { BuilderPriceCounter, BuilderPizzaView },
  props: {
    pizzaName: {
      type: String,
      default: "",
    },
  },
  methods: {
    setName(event) {
      this.$emit("update:pizzaName", event.target.value);
    },
  },
};
</script>

<style scoped></style>
