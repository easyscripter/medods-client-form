<template>
  <div class="easy-select">
    <p class="easy-select-name" @click="isVisible = !isVisible">
      {{ selected }}
    </p>
    <label :for="fieldName">{{ fieldName }}</label>
    <transition name="fade">
      <div v-if="isVisible" class="easy-select-options">
        <p
          @click="selectOption(option)"
          class="easy-select-option"
          v-for="option in options"
          :key="option.value"
        >
          {{ option.name }}
        </p>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "EasySelect",
  props: {
    options: {
      type: Array,
      default() {
        return [];
      },
    },
    selected: {
      type: String,
    },
    fieldName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isVisible: false,
      isClear: false,
    };
  },
  methods: {
    selectOption(option) {
      this.$emit("select", option);
      this.isVisible = false;
    },
    hideSelect() {
      this.isVisible = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.easy-select {
  position: relative;
  width: 100%;
  max-width: 1200px;
  margin-top: 30px;
  padding-right: 8px;
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  outline: none;
  color: gray;
  &-name {
    position: relative;
    width: 100%;
    margin: 0;
    padding-top: 20px;
    padding-bottom: 10px;
    text-align: left;
    border: none;
    border-bottom: 2px solid #8f9399;
    z-index: 6;
    &:after {
      position: absolute;
      content: "";
      width: 8px;
      height: 8px;
      right: 15px;
      top: 20px;
      border-top: 2px solid #000000;
      border-right: 2px solid #000000;
      transform: rotate(135deg);
    }
  }
  &-options {
    position: absolute;
    left: 0;
    top: 40px;
    width: 100%;
    text-align: left;
    z-index: 4;
    -webkit-box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);
    -moz-box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);
    box-shadow: 0 4px 8px 0 rgba(34, 60, 80, 0.2);
    background-color: #fff;
  }
  &-option {
    padding: 5px;
    &:hover {
      background-color: rgba(34, 60, 80, 0.2);
    }
  }
  label {
    display: block;
    position: absolute;
    top: -5px;
    font-size: 16px;
    font-weight: 600;
    text-align: left;
    color: rgba(0, 0, 0, 1);
    transition: top 0.4s ease-in-out;
    pointer-events: none;
  }
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>