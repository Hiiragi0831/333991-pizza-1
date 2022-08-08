<template>
  <div class="counter counter--orange ingredients__counter">
    <button
      type="button"
      class="counter__button counter__button--minus"
      :disabled="isDisabledButtonMinus"
      @changeCount="
        $emit('changeIngredientCount', ingredientCount - 1, ingredientName)
      "
    >
      <span class="visually-hidden">Меньше</span>
    </button>
    <input
      type="text"
      name="counter"
      class="counter__input"
      :value="ingredientCount"
    />
    <button
      type="button"
      class="counter__button counter__button--plus"
      :disabled="isDisabledButtonPlus"
      @changeCount="
        $emit('changeIngredientCount', ingredientCount + 1, ingredientName)
      "
    >
      <span class="visually-hidden">Больше</span>
    </button>
  </div>
</template>

<script>
import { MAX_INGREDIENT_COUNT, MIN_INGREDIENT_COUNT } from "@/constants";
export default {
  name: "ItemCounter",
  props: {
    index: {
      type: Number,
      default: 0,
    },
    ingredientName: {
      type: String,
      default: "",
    },
    ingredientCount: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      count: 0,
      isIngredients: false,
    };
  },
  computed: {
    isDisabledButtonPlus() {
      return this.ingredientCount >= MAX_INGREDIENT_COUNT;
    },
    isDisabledButtonMinus() {
      return this.ingredientCount === MIN_INGREDIENT_COUNT;
    },
  },
};
</script>
