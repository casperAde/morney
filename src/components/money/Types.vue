<template>

  <ul class="types">
    <li :class="value === '-' && 'selected'"
        @click="selectType('-')">支出
    </li>
    <li :class="value === '+' && 'selected'"
        @click="selectType('+')">收入
    </li>
  </ul>

</template>

<script lang="ts">
import Vue from 'vue';
// 提示这是一个组件
import {Component, Prop} from 'vue-property-decorator';

@Component
export default class Types extends Vue {

  @Prop() readonly value!: string;

  selectType(type: string) {
    if (type !== '-' && type !== '+') {
      throw  new Error('type is unknown');
    }
    this.$emit('update:value', type);
  }
}

</script>

<style lang="scss" scoped>
.types {
  background-color: #c4c4c4;
  display: flex;
  text-align: center;
  font-size: 24px;

  > li {
    width: 50%;
    height: 64px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    &.selected {
      &::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 4px;
        background-color: #333;
      }
    }
  }
}
</style>