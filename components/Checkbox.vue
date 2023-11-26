<template>
  <div class="combo-checkbox">
    <button type="button" :class="classes" @click="onClick" :style="style">
      {{ label }}
    </button>
  </div>
</template>
<script>
import { reactive, computed } from "vue";

export default {
  name: "combo-checkbox",

  props: {
    label: {
      type: String,
      required: true,
    },
    primary: {
      type: Boolean,
      default: false,
    },
    size: {
      type: String,
      validator: function (value) {
        return ["small", "medium", "large"].indexOf(value) !== -1;
      },
    },
    backgroundColor: {
      type: String,
    },
  },

  emits: ["click"],

  setup(props, { emit }) {
    props = reactive(props);
    return {
      classes: computed(() => ({
        "combo--primary": props.primary,
        "combo--secondary": !props.primary,
        [`combo--${props.size || "medium"}`]: true,
      })),
      style: computed(() => ({
        backgroundColor: props.backgroundColor,
      })),
      onClick() {
        emit("click");
      },
    };
  },
};
</script>
<style scoped>
.combo-checkbox {
  color: red;
}
</style>
