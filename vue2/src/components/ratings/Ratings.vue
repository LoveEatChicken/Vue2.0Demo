<template>
    <div style="text-align: center;">
      <card-template v-for="(temp, index) in templateData"
                     :desc="temp.desc"
                     :key="index"
                     :name="temp.name"
                     :select-name="selectTemplate"
                     @selectEvent="selectListener"
                     @unSelectEvent="unSelectListener"
      >
      </card-template>
      <div>选中模板：[{{selectTemplate}}]</div>
      <div>
        <div>{{testData.name}}</div>
      </div>
      <div @click="add">增加</div>

      <div @click="show = !show">toggle</div>
      <transition
        enter-active-class="animated jello"
        leave-active-class="animated fadeOutDown"
      >
        <div v-show="show" style="display: inline-block; font-size: 30px">
          Animation
        </div>
      </transition>
    </div>

</template>

<script type="text/ecmascript-6">
  import CardTemplate from '../template_card/TemplateCard.vue'
export default {
  data() {
    return {
      templateData: [
        {desc: 'aaaaaaaaaaaa', 'name': 1},
        {desc: 'bbbbbbbbbbbb', 'name': 2},
        {desc: 'cccccccccccc', 'name': 3},
        {desc: 'dddddddddddd', 'name': 4}
      ],
      selectTemplate: 2,
      testData: {},
      show: false
    }
  },
  components: {
    CardTemplate
  },
  methods: {
    selectListener(selectName) {
      this.selectTemplate = selectName;
//      console.log(this.selectTemplate)
    },
    unSelectListener(unSelectName) {
        if (this.selectTemplate === unSelectName) {
            this.selectTemplate = ''
        }
    },
    add() {
//        this.testData['name'] = 'ccccc';
        this.testData = Object.assign({}, this.testData, {name: 'ccccccc'});
//      this.$set(this.testData, 'name', 'zzzzzzz')
//        console.log(this.testData)
    }
  },
  watch: {
    selectTemplate(val, oldVal) {
        console.log('newSelectName: ' + val);
        console.log('oldSelectName: ' + oldVal);
    }
  }
}
</script>

<style type="text/css">

</style>
