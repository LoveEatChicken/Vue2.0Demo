<template>
  <div :class="[cardSelect ? selectClass : '', defaultClass]" @click="clickCard">
    <div class="under-wrapper">
      <div class="template-title"></div>
      <div class="template-icon"></div>
    </div>
    <div class="opacity-wrapper">
      <div class="template-desc">{{desc}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['name', 'selectName', 'desc'],
    data() {
      return {
        cardSelect: false,
        selectClass: 'card-select',
        defaultClass: 'card-wrapper'
      }
    },
    created() {
//      console.log('created' + this.selectName);
      if (this.selectName === this.name) {
          this.cardSelect = true
      }
    },
    mounted() {
//      console.log('mounted' + this.selectName);
    },
    updated() {
//      console.log('updated' + this.selectName);
    },
    methods: {
      clickCard() {
        this.cardSelect = !this.cardSelect;
        if (this.cardSelect) {
          this.$emit('selectEvent', this.name)
        } else {
          this.$emit('unSelectEvent', this.name)
        }
      }
    },
    watch: {
      selectName(val, oldVal) {
          if (val != this.name) {
            this.cardSelect = false;
          }
      }
    }
  }
</script>

<style type="text/css" scoped>
  .card-wrapper {
    display: inline-block;
    position: relative;
    margin-top: 10px;
    margin-left: 10px;
    border-radius: 2px;
    width: 200px;
    height: 200px;
  }

  .card-select {
    border: 2px solid red;
    border-radius: 3px;
  }

  .under-wrapper, .opacity-wrapper {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
  }

  .under-wrapper {
    background-image: url("pic10.jpg");
    background-size: cover;
  }

  .opacity-wrapper {
    display: table-cell;
    vertical-align: middle;
    opacity: 0;
    transition: opacity .25s ease-in-out, background .25s ease-in-out;
  }

  .opacity-wrapper:hover {
    opacity: 0.9;
    color: #fff;
    background: rgba(0,0,0,0.8);
  }

  .template-desc {
    width: 100%;
    height: 100%;
  }


</style>
