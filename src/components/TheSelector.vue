<template>
  <div class="the-select">
    <div class="the-select__button" @click="showOptions = !showOptions">
      <div v-if="!multiselect && value.label !== ''"><span class="the-select__placeholder">{{value.label}}</span></div>
      <div v-if="multiselect || value.label === ''"><span class="the-select__placeholder">{{placeholder}}</span></div>
      <img
          :src="showOptions ? require('@/assets/arrow-up.svg') : require('@/assets/arrow-down.svg')"
          style="height: 32px; width: 32px"
          alt=""
      />
    </div>
    <div v-if="showOptions" class="the-select__options">
      <div v-for="(option, idx) in options" :key="idx" class="the-select__option" @click="selected(option, idx)">
        {{option.label}}
        <input v-if="checkedArr" v-model="checkedArr[idx]" type="checkbox"/>
      </div>
    </div>
    <div v-if="showCompulsoryErrorMsg && valueIsEmpty" class="input__error-message">
      Это обязательное поле
    </div>
  </div>
</template>

<script>
  import TheInput from "@/components/TheInput.vue"

  export default {
    name: "TheSelect",
    components: {TheInput},
    props: {
      value: {
        type: [Object, Array],
        required: true
      },
      options: {
        type: Array,
        required: true
      },
      placeholder: {
        type: String,
        default: ""
      },
      multiselect: {
        type: Boolean,
        default: false,
      },
      compulsory: {
        type: Boolean,
        default: false
      },
      showCompulsoryErrorMsg: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        showOptions: false,
        checkedArr: null
      }
    },
    created() {
      this.checkedArr = this.multiselect
          ? this.options.map(option => this.value?.some(val => val.value === option.value) || false)
          : null
    },
    computed: {
      valueIsEmpty() {
        if (this.multiselect) {
          return this.value?.length === 0
        }
        return !this.value.value
      }
    },
    methods: {
      selected(val, idx) {
        if (this.multiselect) {
          const present = this.checkedArr[idx]
          this.checkedArr[idx] = !this.checkedArr[idx]
          if (!present) {
            this.value.push(val)
            return
          }
          this.value.splice(idx, 1)
          return
        }
        this.showOptions = !this.showOptions
        this.$emit("input", val)
      }
    }
  }
</script>

<style scoped>
.the-select {
  position: relative;
  width: 100%;
  max-width: 400px;
  margin-bottom: 20px;
}

.the-select__button {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: 397px;
  font-size: .75em;
  height: 45px;
  border-radius: 10px;
  border: 1px solid #43799b;
  background-color: white;
}

.the-select__placeholder {
  margin-left: 10px;
}

.the-select__options {
  background-color: white;
  cursor: pointer;
  border: 1px solid #43799b;
  width: 100%;
  border-radius: 10px;
  font-size: .75em;
  position: absolute;
  z-index: 2;
}

.the-select__option {
  padding: 0 10px 0 10px;
  justify-content: space-between;
  display: flex;
}

.the-select__option:first-child {
  border-radius: 10px 10px 0 0;
}
.the-select__option:last-child {
  border-radius: 0 0 10px 10px;
}

.the-select__option:hover{
  background-color: #85c2e2;
}
.input__error-message{
  color: darkred;
  font-size: 12px;
  text-wrap: normal;
  text-align: left;
  width: 100%;
}
</style>