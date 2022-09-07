<template>
  <div class="content__ingredients">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите ингредиенты</h2>

      <div class="sheet__content ingredients">
        <div class="ingredients__sauce">
          <p>Основной соус:</p>

          <label
            class="radio ingredients__input"
            v-for="{ id, name, value } in sauces"
            :key="id"
            :title="name"
          >
            <input
              type="radio"
              name="sauce"
              :value="value"
              :checked="selectedSauces.id === id"
              @click="updateSauces({ id, name, value })"
            />
            <span>{{ name }}</span>
          </label>
        </div>

        <div class="ingredients__filling">
          <p>Начинка:</p>

          <ul class="ingredients__list">
            <li
              class="ingredients__item"
              v-for="{ id, name, value } in ingredients"
              :key="id"
              :title="name"
            >
              <AppDrop @drop="$emit('drop', $event)">
                <AppDrag
                  :ingredient-name="name"
                  :ingredient-count="
                    getIngredientCount(name, selectedIngredients)
                  "
                >
                  <span class="filling" :class="`filling--${value}`">
                    {{ name }}
                  </span>
                </AppDrag>
              </AppDrop>

              <item-counter
                :ingredient-count="
                  getIngredientCount(name, selectedIngredients)
                "
                @changeIngredientCount="changeIngredientCount($event, name)"
              />
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ItemCounter from "@/common/components/ItemCounter";
import AppDrag from "@/common/components/AppDrag";
import AppDrop from "@/common/components/AppDrop";

export default {
  name: "BuilderIngredientsSelector",
  components: { ItemCounter, AppDrag, AppDrop },
  props: {
    ingredients: {
      type: Array,
      required: true,
    },
    sauces: {
      type: Array,
      required: true,
    },
    selectedSauces: {
      type: Object,
      required: true,
    },
    selectedIngredients: {
      type: Object,
      required: true,
    },
  },
  methods: {
    updateSauces(event) {
      this.$emit("update:selectedSauces", event);
    },
    getIngredientCount(ingredientName, selectedIngredients) {
      return selectedIngredients[ingredientName]
        ? selectedIngredients[ingredientName]
        : 0;
    },
    changeIngredientCount(count, name) {
      this.$emit("update:selectedIngredients", name, count);
    },
  },
};
</script>
