<template>
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
            :checked="selectedDough.id === id"
            @click="updateDough({ id, name, description, value })"
          />
          <b>{{ name }}</b>
          <span>{{ description }}</span>
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BuilderDoughSelector",
  props: {
    dough: {
      type: Array,
      required: true,
    },
    selectedDough: {
      type: Object,
      required: true,
    },
  },
  methods: {
    updateDough(event) {
      this.$emit("update:selectedDough", event);
    },
  },
};
</script>

<style scoped></style>
