<template>
  <main class="content">
    <form action="#" method="post">
      <div class="content__wrapper">
        <h1 class="title title--big">Конструктор пиццы</h1>

        <div class="content__dough">
          <div class="sheet">
            <h2 class="title title--small sheet__title">Выберите тесто</h2>

            <div class="sheet__content dough">
              <label
                class="dough__input"
                v-for="{ id, name, description, value } in dough"
                :class="`dough__input--${value}`"
                :key="id"
                :title="name"
              >
                <input
                  type="radio"
                  name="dought"
                  :value="value"
                  class="visually-hidden"
                  checked
                />
                <b>{{ name }}</b>
                <span>{{ description }}</span>
              </label>
            </div>
          </div>
        </div>

        <div class="content__diameter">
          <div class="sheet">
            <h2 class="title title--small sheet__title">Выберите размер</h2>

            <div class="sheet__content diameter">
              <label
                class="diameter__input"
                v-for="{ id, name, value } in sizes"
                :class="`diameter__input--${value}`"
                :key="id"
                :title="name"
              >
                <input
                  type="radio"
                  name="diameter"
                  :value="value"
                  class="visually-hidden"
                />
                <span>{{ name }}</span>
              </label>
            </div>
          </div>
        </div>

        <div class="content__ingredients">
          <div class="sheet">
            <h2 class="title title--small sheet__title">
              Выберите ингредиенты
            </h2>

            <div class="sheet__content ingredients">
              <div class="ingredients__sauce">
                <p>Основной соус:</p>

                <label
                  class="radio ingredients__input"
                  v-for="{ id, name, value } in sauces"
                  :key="id"
                  :title="name"
                >
                  <input type="radio" name="sauce" :value="value" />
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
                    <span class="filling" :class="`filling--${value}`">
                      {{ name }}
                    </span>

                    <div class="counter counter--orange ingredients__counter">
                      <button
                        type="button"
                        class="counter__button counter__button--minus"
                        disabled
                      >
                        <span class="visually-hidden">Меньше</span>
                      </button>
                      <input
                        type="text"
                        name="counter"
                        class="counter__input"
                        value="0"
                      />
                      <button
                        type="button"
                        class="counter__button counter__button--plus"
                      >
                        <span class="visually-hidden">Больше</span>
                      </button>
                    </div>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>

        <div class="content__pizza">
          <label class="input">
            <span class="visually-hidden">Название пиццы</span>
            <input
              type="text"
              name="pizza_name"
              placeholder="Введите название пиццы"
            />
          </label>

          <div class="content__constructor">
            <div class="pizza pizza--foundation--big-tomato">
              <div class="pizza__wrapper">
                <div class="pizza__filling pizza__filling--ananas"></div>
                <div class="pizza__filling pizza__filling--bacon"></div>
                <div class="pizza__filling pizza__filling--cheddar"></div>
              </div>
            </div>
          </div>

          <div class="content__result">
            <p>Итого: 0 ₽</p>
            <button type="button" class="button" disabled>Готовьте!</button>
          </div>
        </div>
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

export default {
  name: "IndexHome",
  data() {
    return {
      pizza,
    };
  },
  computed: {
    dough() {
      return this.pizza.dough.map((dough) => ({
        ...dough,
        value: doughValues[dough.name],
      }));
    },
    ingredients() {
      return this.pizza.ingredients.map((ingredient) => ({
        ...ingredient,
        value: ingredientValues[ingredient.name],
      }));
    },
    sauces() {
      return this.pizza.sauces.map((sauce) => ({
        ...sauce,
        value: saucesValues[sauce.name],
      }));
    },
    sizes() {
      return this.pizza.sizes.map((sizes) => ({
        ...sizes,
        value: sizesValues[sizes.name],
      }));
    },
  },
};
</script>

<style lang="scss" scoped></style>
