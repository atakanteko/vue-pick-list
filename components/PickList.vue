<template>
  <div>
    <h1>{{ title }}</h1>

    <div style="display: flex; align-items: center">
      <div :class="{'checkbox-outer-box':getSelectedCheckboxCount===0,'checkbox-outer-wide-box':getSelectedCheckboxCount>0}">
        <input :id="targetSide"
               type="checkbox"
               :checked="isAnyCheckBoxSelected"
               :disabled="checkAnyBoxSelectedInLeftSide > 0 || checkAnyBoxSelectedInRightSide > 0"
               @change="selectAll($event)"
        >
        <label :for="targetSide" v-if="getSelectedCheckboxCount===0"></label>
        <label :for="targetSide" v-else-if="getSelectedCheckboxCount === value.filter(item => !item.done).length">Tümü Seçildi</label>
        <label :for="targetSide" v-else>{{getSelectedCheckboxCount}} adet seçildi</label>

      </div>
      <span style="line-height: normal;"> {{ isAnyCheckBoxSelected ? 'Tümünü Kaldır' : 'Tümünü Seç' }}</span>
    </div>

    <div class="mb-12 container-scrollable pr-2" style="padding-top: 14px">
      <div class="custom-scroll" style="color:black;max-height: 608px; overflow-y: auto; padding-top: 12px">
        <div v-for="(item, index) in value" :key="item.id" :class="{'mb-4': index !== (value.length-1)}">
            <input
              :id="item.id"
              v-model="item.currentStatus"
              type="checkbox"
              :checked="item.done"
              :disabled="item.done || checkAnyBoxSelectedInLeftSide > 0 || checkAnyBoxSelectedInRightSide > 0"
            >
            <label :for="item.id">{{item.todo}}</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'PickList',
  props: {
    targetSide: {
      type: String
    },
    title: {
      type: String,
      default: ''
    },
    value: {
      type: Array,
    },
    checkAnyBoxSelectedInLeftSide: {
      type: Number,
    },
    checkAnyBoxSelectedInRightSide: {
      type: Number,
    }
  },
  methods: {
    selectAll(event){
      this.value.filter(item => {
        if (!item.done) {
          item.currentStatus = event.target.checked
        }
      })
    }
  },
  computed: {
    getSelectedCheckboxCount() {
      return this.value.filter(item => item.currentStatus && !item.done).length
    },
    isAnyCheckBoxSelected() {
      return this.value.some(item => item.currentStatus && !item.done);
    },
  },
};
</script>
<style scoped lang="scss">
label{
  color: black;
}
.container-scrollable {
  /*padding-top: 26px;*/
  padding-left: 24px;
  border-radius: 5px !important;
  border: 1px solid #EAEAEA !important;
  background-color: #FFFFFF;
  max-width: 363px;
  height: 638px;
}
.checkbox-outer-box {
  width: 40px;
  height: 40px;
  margin: 24px 8px 20px 0px;
  padding: 7px;
  border-radius: 5px;
  border: solid 1px #eaeaea;
  background-color: #fff;
}

.checkbox-outer-wide-box{
  width: 140px;
  height: 40px;
  margin: 24px 8px 20px 16px;
  padding: 7px;
  border-radius: 5px;
  border: solid 1px #eaeaea;
  background-color: #fff;
}
</style>


