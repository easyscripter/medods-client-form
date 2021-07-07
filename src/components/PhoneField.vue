<template>
  <div class="PhoneField">
    <input
      type="tel"
      required
      :id="fieldName"
      name="inputField"
      placeholder="+7 (999) 555-55-55"
      :value="value"
      @input="$emit('input', $event.target.value)"
      pattern="^\+7\s?[0-7|9]?[0-9]{2}\s?[0-9]{3}\s?[0-9]{2}\s?[0-9]{2}"
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
    nameColor: {
      type: String,
      default() {
        "#000000";
      },
    },
  },
  data: () => {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.PhoneField {
  width: 100%;
  position: relative;
  display: inline-block;
  margin-top: 10px;
  margin-bottom: 28px;
  font-family: "Roboto", sans-serif;
  font-weight: normal;
}

label,
input {
  display: block;
}

label {
  position: absolute;
  top: 2px;
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
  padding-bottom: 10px;
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
