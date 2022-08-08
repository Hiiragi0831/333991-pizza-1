<template>
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
            :checked="selectedSizes.id === id"
            @click="updateSizes({ id, name, value })"
            class="visually-hidden"
          />
          <span>{{ name }}</span>
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BuilderSizeSelector",
  props: {
    sizes: {
      type: Array,
      required: true,
    },
    selectedSizes: {
      type: Object,
      required: true,
    },
  },
  methods: {
    updateSizes(event) {
      this.$emit("update:selectedSizes", event);
    },
  },
};
</script>
