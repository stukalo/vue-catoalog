<template>
  <div class='toggle'>
    <div class='toggle_title'>
      <span>{{ title }}</span>
    </div>
    <ul class="toggle_options options">
      <li class='options_item'
          v-for="option in options"
          v-bind:class="option.active && 'active'"
          :key="option.value"
          @click="this.onChange(option.value)"
      >
        <span>
          {{ option.text }}
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Toggle',
  props: {
    title: { type: String, default: '' },
    options: { type: Array, default: [] },
  },
  methods: {
    onChange(value) {
      this.$emit('change', value);
    },
  },
};
</script>

<style scoped lang="less">
@import (reference) '../../assets/css/variables.less';
@import (once) '../../assets/css/reset.less';

.toggle {
  display: flex;
  width: fit-content;
  align-items: center;
  .fontMixin(18px);
  color: @primaryText;
  text-transform: uppercase;
}

.toggle_title {
  margin-right: 20px;
}

.toggle_options {
  display: flex;
  list-style: none;
  background-color: @secondaryBackgroundOpacity;
  border-radius: @primaryBorderRadius;
  overflow: hidden;
}

.options_item {
  padding: 0 20px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  background-color: @primaryBackgroundOpacity;

  &.active {
    background-color: @activeBackground;
  }
}

@media only screen and (max-width: 600px) {
  .toggle {
    flex-direction: column;
    width: auto;
  }

  .toggle_title {
    margin: 0 0 15px 0;
  }
}

</style>
