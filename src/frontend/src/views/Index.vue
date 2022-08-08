<template>
  <main class="content">
    <form action="#" method="post">
      <div class="content__wrapper">
        <h1 class="title title--big">Конструктор пиццы</h1>
        <builder-dough-selector
          :dough="dough"
          :selectedDough.sync="selectedDough"
        />

        <builder-size-selector
          :sizes="sizes"
          :selectedSizes.sync="selectedSizes"
        />

        <builder-ingredients-selector
          :ingredients="ingredients"
          :sauces="sauces"
          :selectedSauces.sync="selectedSauces"
          :selectedIngredients.sync="selectedIngredients"
        />

        <builder-content-pizza :pizzaName.sync="pizzaName" />
      </div>
    </form>
  </main>
</template>

<script>
import pizza from "@/static/pizza.json";
import saucesValues from "@/common/enums/saucesValues.js";
import doughValues from "@/common/enums/doughValues.js";
import ingredientValues from "@/common/enums/ingredientValues.js";
import sizesValues from "@/common/enums/sizesValues";
import BuilderDoughSelector from "@/modules/builder/BuilderDoughSelector";
import BuilderSizeSelector from "@/modules/builder/BuilderSizeSelector";
import BuilderIngredientsSelector from "@/modules/builder/BuilderIngredientsSelector";
import BuilderContentPizza from "@/modules/builder/BuilderContentPizza";

export default {
  name: "IndexHome",
  components: {
    BuilderContentPizza,
    BuilderIngredientsSelector,
    BuilderSizeSelector,
    BuilderDoughSelector,
  },
  data() {
    return {
      pizzaName: "",
      selectedDough: {},
      selectedSizes: {},
      selectedSauces: {},
      selectedIngredients: {},
    };
  },
  mounted() {
    this.selectedDough = this.dough[0] || null;
    this.selectedSizes = this.sizes[0] || null;
    this.selectedSauces = this.sauces[0] || null;
  },
  computed: {
    dough() {
      return pizza.dough.map((dough) => ({
        ...dough,
        value: doughValues[dough.name],
      }));
    },
    ingredients() {
      return pizza.ingredients.map((ingredient) => ({
        ...ingredient,
        value: ingredientValues[ingredient.name],
      }));
    },
    sauces() {
      return pizza.sauces.map((sauce) => ({
        ...sauce,
        value: saucesValues[sauce.name],
      }));
    },
    sizes() {
      return pizza.sizes.map((sizes) => ({
        ...sizes,
        value: sizesValues[sizes.name],
      }));
    },
  },
};
</script>

<style lang="scss" scoped></style>
