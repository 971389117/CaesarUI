<template>
  <button class="g-button" :class="{[`icon-${iconPosition}`]:true}" @click="$emit('click')">
    <g-icon class='icon' v-if="icon && !loading" :name='icon'></g-icon>
    <g-icon class='icon loading' v-if="loading" name='loading'></g-icon>
    <div class="g-button-content">
      <slot></slot>
    </div>
  </button>
</template>
<script>
import Icon from "../icon";
export default {
  name: "GuluButton",
  components: {
    "g-icon": Icon
  },
  props: {
    icon: {},
    loading: {
      type: Boolean,
      default: false
    },
    iconPosition: {
      type: String,
      default: "left",
      validator(value) {
        return value === "left" || value === "right";
      }
    }
  }
};
</script>
<style lang="scss" scoped>
@import "var";
.g-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0 1em;
  height: $button-height;
  border: 1px solid $border-color;
  border-radius: $border-radius;
  background: $button-bg;
  vertical-align: middle;
  font-size: $font-size;
  &:hover {
    border-color: $border-color-hover;
  }
  &:active {
    background-color: $button-active-bg;
  }
  &:focus {
    outline: none;
  }
  > .g-button-content {
    order: 2;
  }
  > .icon {
    order: 1;
    margin-right: 0.1em;
  }

  &.icon-right {
    > .g-button-content {
      order: 1;
    }
    > .icon {
      order: 2;
      margin-right: 0;
      margin-left: 0.1em;
    }
  }
  .loading {
    @include spin;
  }
}
</style>
