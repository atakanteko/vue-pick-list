<template>
  <div class="d-flex justify-space-between">
  <v-row >
    <v-col style="max-width: 387px">
      <PickList
        :title="leftTitle"
        v-model="getTodos"
        targetSide="leftSide"
        :checkAnyBoxSelectedInRightSide="getNumberOfTodosThatIsSelectedInRight"
      />
    </v-col>
    <v-col class="col-1" style="max-width: 30px;margin:0 12px;">
      <div style="display: flex;flex-direction: column;align-items: center;margin-top: 371px">
        <div>
          <button
            @click="moveSelectedTodosRightCard"
            class="btn-mdl"
            style="color:black;margin-bottom:16px;position: relative"
            :class="{'active':getNumberOfTodosThatIsSelectedInLeft,'pointer-events':getNumberOfTodosThatIsSelectedInRight || !getNumberOfTodosThatIsSelectedInLeft}"
          >
            >
          </button>
        </div>
        <div>
          <button
            class="btn-mdl"
            style="position: relative;color:black"
            @click="moveSelectedTodosLeftCard"
            :class="{'active':getNumberOfTodosThatIsSelectedInRight,'pointer-events':getNumberOfTodosThatIsSelectedInLeft || !getNumberOfTodosThatIsSelectedInRight}"
          >
            <
          </button>
        </div>
      </div>
    </v-col>
    <v-col style="width: 650px">
      <PickList
        :title="rightTitle"
        v-model="getDoneTodos"
        targetSide="rightSide"
        :checkAnyBoxSelectedInLeftSide="getNumberOfTodosThatIsSelectedInLeft"
      />
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
  methods: {
    isAnyCheckboxSelectedInLeftCard(){

    },
    moveSelectedTodosLeftCard() {
      const todosSelectedByUser = this.value.filter(item => item.currentStatus && !item.done);
      todosSelectedByUser.forEach(item => {
        item.isSelected = false
      })
    },
    moveSelectedTodosRightCard() {
      const todosSelectedByUser = this.value.filter(item => item.currentStatus);
      todosSelectedByUser.forEach(item => {
        item.isSelected = true
      })
    }
  },
  computed: {
    getDoneTodos() {
      return this.value.filter(item => item.isSelected)
    },
    getTodos() {
      return this.value.filter(item => !item.isSelected)
    },
    getNumberOfTodosThatIsSelectedInLeft() {
      return this.value.filter(item => item.currentStatus && !item.isSelected).length
    },
    getNumberOfTodosThatIsSelectedInRight() {
      return this.value.filter(item => item.currentStatus && item.isSelected && !item.done).length
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
.active{
  background: #f7ca27;
  border-color: #f7ca27;
}
.pointer-events{
  pointer-events: none;
}
</style>
