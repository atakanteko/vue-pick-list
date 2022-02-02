<template>
  <div class="d-flex justify-space-between">
  <v-row >
    <v-col style="max-width: 387px">
      <PickList
        :title="leftTitle"
        v-model="getTodos"/>
    </v-col>
    <v-col class="col-1" style="max-width: 30px;margin:0 12px;">
      <div style="display: flex;flex-direction: column;align-items: center;margin-top: 371px">
        <div>
          <button
            class="btn-mdl"
            style="color:black;margin-bottom:16px;position: relative">
            >
          </button>
        </div>
        <div>
          <button
            class="btn-mdl"
            style="position: relative;color:black"
          >
            <
          </button>
        </div>
      </div>
    </v-col>
    <v-col style="width: 650px">
      <PickList
        :title="rightTitle"
        v-model="getDoneTodos"/>
    </v-col>
  </v-row>
  </div>
</template>

<script>
import PickList from "./PickList";
export default {
  name: 'PickListContainer',
  components: {
    PickList,
  },
  data() {
    return {
      leftTitle: 'Yapılacaklar',
      rightTitle: 'Tamamlananlar',
    }
  },
  props: {
    value: {
      type: Array,
      default: []
    },
  },
  computed: {
    getDoneTodos() {
      return this.value.filter(item => item.isSelected)
    },
    getTodos() {
      return this.value.filter(item => !item.isSelected)
    }
  },
};
</script>
<style scoped>
.btn-mdl {
  width: 30px;
  height: 44px;
  border-radius: 5px !important;
  border: 1px solid #EAEAEA !important;
  background-color: #FFFFFF;
}
</style>
