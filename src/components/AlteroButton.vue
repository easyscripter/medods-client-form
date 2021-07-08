<template>
  <button
    @click.prevent="$emit('clickOnButton')"
    :style="{
      backgroundColor: bgColor,
      boxShadow: `7px 4px 17px 3px ${shadowColor}`,
    }"
  >
    {{ buttonText }}
  </button>
</template>

<script>
export default {
  props: {
    buttonText: {
      type: String,
      required: true,
    },
    bgColor: {
      type: String,
    },
    shadowColor: {
      type: String,
    },
    pressedButton: {
      type: Boolean,
    },
  },
  data: () => {
    return {
      activeButton: false,
    };
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
button {
  position: relative;
  margin-top: 20px;
  margin-bottom: 20px;
  padding: 14px 40px;
  background: #f47719;
  border-radius: 5px;
  outline: none;
  border: none;
  font-size: 16px;
  font-weight: bold;
  color: #000000;
  cursor: pointer;
  transition: all 0.7s ease-out;
  border: 1px solid #000000;

  &:active {
    box-shadow: 7px 2px 17px 3px #8413b3;
    color: #8413b3;
  }
}
</style>
