<template>
  <div class="DateField">
    <input
      type="date"
      :id="fieldName"
      name="inputField"
      :placeholder="fieldPlaceholder"
      :value="value"
      @input="$emit('input', $event.target.value)"
    />
    <label :for="fieldName" :style="{ color: nameColor }">{{
      fieldName
    }}</label>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true,
    },
    fieldName: {
      type: String,
      required: true,
    },
    fieldPlaceholder: {
      type: String,
    },
    nameColor: {
      type: String,
    },
  },
  components: {},
  data: () => {
    return {};
  },
};
</script>
<style lang="scss" scoped>
.DateField {
  width: 100%;
  position: relative;
  display: inline-block;
  margin-top: 10px;
  margin-bottom: 18px;
  font-family: "Roboto", sans-serif;
  font-weight: normal;
}

label,
input {
  display: block;
}

label {
  position: absolute;
  top: 5px;
  font-size: 16px;
  font-weight: 600;
  text-align: left;
  color: rgba(0, 0, 0, 1);
  transition: top 0.4s ease-in-out;
  pointer-events: none;
}

input {
  position: relative;
  width: 100%;
  margin-top: 9px;
  padding-top: 20px;
  padding-bottom: 5px;
  font-family: "Roboto", sans-serif;
  font-weight: bold;
  color: #000000;
  border: none;
  border-bottom: 2px solid #8f9399;
  background: transparent;
  transition: border-bottom-color 0.4s ease-in-out;
  &:focus {
    outline: none;
    border-bottom-color: #39078d;
  }
}

.icon {
  position: absolute;
  top: 34px;
  right: 10px;

  img {
    max-width: 23px;
    max-height: 23px;
  }
}
</style>