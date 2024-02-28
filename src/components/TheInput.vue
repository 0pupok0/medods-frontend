<template>
  <div :class="['input', {'input_invalid': invalid || showCompulsoryErrorMsg}]">
    <div class="input__label">
      {{label}}<template v-if="compulsory">*</template>
    </div>
    <div v-if="type === 'text' || type === 'number'" class="input__body">
      <input class="input__body_field" v-model="localValue">
    </div>
    <div v-if="type === 'checkbox'">
      <input v-model="localValue" type="checkbox">
    </div>
    <div v-if="type === 'radio'">
      <input v-model="localValue" type="radio">
    </div>
    <div v-if="type === 'date'" class="input__body">
      <input v-model="localValue" class="input__body_field" type="date" lang="ru">
    </div>
    <div v-if="invalid" class="input__error-message">
      {{errorMsg}}
    </div>
    <div v-if="showCompulsoryErrorMsg && value === ''" class="input__error-message">
      Это обязательное поле
    </div>
  </div>
</template>

<script>
  export default{
    name: "TheInput",
    props:{
      value:{
        type: [String, Boolean, null],
        required: true
      },
      label: {
        type: String,
        default: ""
      },
      type:{
        type: String,
        default: "text"
      },
      invalid:{
        type: Boolean,
        default: false,
      },
      errorMsg:{
        type: String,
        default: "",
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
    data(){
      return{
        localValue: null,
      }
    },
    created(){
      this.localValue = this.value
    },
    watch:{
      localValue(){
        if (this.localValue === this.value){
          return
        }
        if (this.type !== "number" || /^[0-9]+$/.test(this.localValue)) {
          this.$emit("input", this.localValue)
          return
        }
        this.localValue = this.value
      },
      value(){
        this.localValue = this.value
      }
    }
  }
</script>

<style scoped>
.input {
  display: flex;
  width: 100%;
  max-width: 400px;
  text-align: left;
  align-items: center;
  flex-direction: column;
  margin-bottom: 25px;
}

.input.input_invalid {
  margin-bottom: 5px;
}

.input__body {
  width: 100%;
}

.input__body_field{
  font-family: Rateway,serif;
  width: calc(100% - 12px);
  height: 45px;
  border-radius: 10px;
  border: 1px solid #43799b;
  font-size: .75em;
  padding: 0 0 0 10px;
}

.input_invalid .input__body_field {
  border: 1px solid darkred;
}

.input__label {
  width: 100%;
}

.input__error-message{
  color: darkred;
  font-size: 12px;
  text-wrap: normal;
  text-align: left;
  width: 100%;
}
</style>