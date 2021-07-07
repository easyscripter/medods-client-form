<template>
  <div class="easy-select-multiple">
    <select
      class="easy-select-multiple__text"
      multiple
      @mousedown.prevent="onSelect"
    >
      <slot></slot>
    </select>
    <label class="easy-select-multiple__label">{{ fieldName }}</label>
    <span class="easy-select-multiple__highlight"></span>
    <span class="easy-select-multiple__bar"></span>
  </div>
</template>

<script>
export default {
  name: "EasySelect",
  props: {
    items: {
      type: Array,
      default() {
        return [];
      },
    },
    value: {
      type: String,
    },
    fieldName: {
      type: String,
      required: true,
    },
  },
  watch: {
    value: {
      immediate: true,
      handler(v) {
        this.$nextTick(() =>
          this.$el
            .querySelectorAll("option")
            .forEach((n) => (n.selected = v.includes(n.value)))
        );
      },
    },
  },
  methods: {
    onSelect(e) {
      this.$el.focus();
      if (e.target.tagName === "OPTION") {
        const v = e.target.value;
        this.$emit(
          "input",
          this.value.includes(v)
            ? this.value.filter((n) => n !== v)
            : [...this.value, v]
        );
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.easy-select-multiple {
  display: grid;
  grid-template-areas: "select";
  align-items: center;
  position: relative;

  &__text {
    appearance: none;
    background-color: transparent;
    border: none;
    padding: 0 1em 0 0;
    margin: 0;
    width: 100%;
    font-family: inherit;
    font-size: inherit;
    cursor: inherit;
    line-height: inherit;
    z-index: 1;
    &::-ms-expand {
      display: none;
    }
    outline: none;
  }
}
</style>