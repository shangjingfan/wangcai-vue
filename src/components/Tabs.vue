<template>
  <div>
    <ul class="tabs" :class="[classPrefix + '-tabs']">
      <li
        v-for="item in dataSource"
        :key="item.value"
        class="tabs-item"
        :class="liClass(item)"
        @click="select(item)"
      >
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";

type DataSourceItem = {
  text: string;
  value: string;
};

@Component
export default class Tabs extends Vue {
  @Prop({ required: true, type: Array })
  dataSource!: DataSourceItem[];

  @Prop(String)
  readonly value!: string;

  @Prop(String)
  classPrefix?: string;

  liClass(item: DataSourceItem) {
    return {
      selected: item.value === this.value,
      [this.classPrefix + "-tabs-item"]: this.classPrefix,
    };
  }

  select(item: DataSourceItem) {
    this.$emit("update:value", item.value);
  }
}
</script>

<style scoped lang="scss">
.tabs {
  background: #a1b4c2;
  display: flex;
  text-align: center;
  justify-content: center;
  font-size: 24px;

  &-item {
    width: 20%;
    height: 64px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    &.selected::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      border-bottom: 5px solid #333333;
    }
  }
}
</style>