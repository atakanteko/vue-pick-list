<template>
  <div>
    <h1>{{ title }}</h1>

    <div style="display: flex; align-items: center">
      <div class="checkbox-outer-box">
      </div>
      <span style="line-height: normal;">Tümünü Kaldır</span>
    </div>

    <div class="mb-12 container-scrollable pr-2" style="padding-top: 14px">
      <div class="custom-scroll" style="color:black;max-height: 608px; overflow-y: auto; padding-top: 12px">
        <div v-for="(item, index) in value" :key="item.id" :class="{'mb-4': index !== (value.length-1)}">
            <input
              :id="item.id"
              v-model="item.currentStatus"
              type="checkbox"
              :checked="item.done"
              :disabled="item.done"
              @change="toggleChecked"
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
    title: {
      type: String,
      default: ''
    },
    value: {
      type: Array,
    }
  },
  methods: {
    toggleChecked() {
      console.log(this.value)
    }
  },
};
</script>
<style scoped lang="scss">
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
  margin: 24px 8px 20px 16px;
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


