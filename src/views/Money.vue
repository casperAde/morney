<template>

  <Layout class-prefix="layout">
    <Tags/>
    <div class="notes">
      <FormItem field-name="备注"
                placeholder="在这里输入备注"
                @update:value="onUpdateNotes"
      />
    </div>
    <Types :value.sync="record.type"/>
    <NumberPad :value.sync="record.amount" @submit="saveRecord"/>

  </Layout>

</template>

<script lang="ts">
import Vue from 'vue';
import NumberPad from '@/components/money/NumberPad.vue';
import Types from '@/components/money/Types.vue';
import FormItem from '@/components/money/FormItem.vue';
import Tags from '@/components/money/Tags.vue';
import {Component} from 'vue-property-decorator';
import store from '@/store/index2';

console.log('我在vue-memory');

@Component({
  components: {Tags, FormItem, Types, NumberPad},
  computed: {
    recordList() {
      return store.recordList;
    }
  }
})
export default class Money extends Vue {

  // 收集相关区域的值
  record: RecordItem = {
    tags: [], notes: '', type: '-', amount: 0
  };

  onUpdateNotes(value: string) {
    this.record.notes = value;
  }

  saveRecord() {
    store.createRecord(this.record);
  }

}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column;

}

.notes {
  padding: 12px 0;
}
</style>

<style lang="scss">
@import "~@/assets/style/helper.scss";
</style>

