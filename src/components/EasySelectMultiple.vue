<template>
  <div class="easy-multiselect">
    <div class="selectBox" @click="showCheckboxes">
      <select>
        <option v-if="groups.length < 1">{{ fieldName }}</option>
        <option v-else>{{ groups.toString() }}</option>
      </select>
      <div class="overSelect"></div>
    </div>
    <div id="checkboxes">
      <div v-for="(item, index) in items" :key="index" class="checkbox">
        <input
          :value="item"
          v-model="groups"
          type="checkbox"
          :id="`checkbox-${index}`"
        />
        <label :for="`checkbox-${index}`">{{ item }}</label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "EasySelectMultiple",
  props: {
    items: {
      type: Array,
      default() {
        return [];
      },
    },
    fieldName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      expanded: false,
      groups: [],
    };
  },
  methods: {
    showCheckboxes() {
      let checkboxes = document.getElementById("checkboxes");
      if (!this.expanded) {
        checkboxes.style.display = "block";
        this.expanded = true;
      } else {
        checkboxes.style.display = "none";
        this.expanded = false;
        this.$emit("getValues", this.groups);
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.easy-multiselect {
  font-family: "Roboto", "Helvetica", "Arial", sans-serif;
  position: relative;
  width: 100%;
  max-width: 1200px;
  margin-top: 40px;
}

.selectBox {
  position: relative;
}

.selectBox select {
  position: relative;
  font-family: inherit;
  background-color: transparent;
  width: 100%;
  max-width: 1200px;
  padding: 10px 10px 10px 0;
  font-size: 18px;
  border-radius: 0;
  border: none;
  border-bottom: 1px solid rgba(0, 0, 0, 0.75);
}

.overSelect {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}

#checkboxes {
  display: none;
  border: 1px #dadada solid;
  text-align: left;
}

#checkboxes label {
  padding: 12px 30px;
  width: inherit;
  display: block;
  text-align: left;
  color: #3c454c;
  font-weight: bold;
  cursor: pointer;
  position: relative;
  z-index: 2;
  transition: color 200ms ease-in;
  overflow: hidden;

  &:before {
    width: 100%;
    height: 10px;
    border-radius: 50%;
    content: "";
    background-color: #5562eb;
    position: absolute;
    left: 40%;
    top: 40%;
    transform: translate(-50%, -50%) scale3d(1, 1, 1);
    transition: all 300ms cubic-bezier(0.4, 0, 0.2, 1);
    opacity: 0;
    z-index: -1;
  }

  &:after {
    width: 12px;
    height: 12px;
    content: "";
    border: 2px solid #d1d7dc;
    background-color: #fff;
    background-image: url("data:image/svg+xml,%3Csvg width='32' height='32' viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M5.414 11L4 12.414l5.414 5.414L20.828 6.414 19.414 5l-10 10z' fill='%23fff' fill-rule='nonzero'/%3E%3C/svg%3E ");
    background-repeat: no-repeat;
    background-position: 2px 3px;
    border-radius: 50%;
    z-index: 2;
    position: absolute;
    left: 10px;
    top: 50%;
    transform: translateY(-50%);
    cursor: pointer;
    transition: all 200ms ease-in;
  }
}

#checkboxes input {
  width: 32px;
  height: 32px;
  order: 1;
  z-index: 2;
  position: absolute;
  right: 30px;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  visibility: hidden;

  &:checked ~ label {
    color: #fff;

    &:before {
      transform: translate(-50%, -50%) scale3d(56, 56, 1);
      opacity: 1;
    }

    &:after {
      background-color: #54e0c7;
      border-color: #54e0c7;
    }
  }
}
</style>