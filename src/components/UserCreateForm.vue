<template>
  <div class="user-create-form">
    <the-input
      v-model="LastName"
      :invalid="textIsInvalid(LastName)"
      label="Фамилия"
      type="text"
      class="the-input"
      error-msg="Фамилия может содержать только буквы кириллицы и латинского алфавита и тире"
      compulsory
      :show-compulsory-error-msg="showCompulsoryErrorMsg"
      />
    <the-input
        v-model="Name"
        :invalid="textIsInvalid(Name)"
        label="Имя"
        type="text"
        class="the-input"
        error-msg="Имя может содержать только буквы кириллицы и латинского алфавита и тире"
        compulsory
        :show-compulsory-error-msg="showCompulsoryErrorMsg"
    />
    <the-input
        v-model="Patronymic"
        :invalid="textIsInvalid(Patronymic)"
        label="Отчество"
        type="text"
        class="the-input"
        error-msg="Отчество может содержать только буквы кириллицы и латинского алфавита и тире"
    />
    <the-input
        v-model="BirthDate"
        label="Дата рождения"
        type="date"
        class="the-input__type-date"
        compulsory
        :show-compulsory-error-msg="showCompulsoryErrorMsg"
    />
    <the-input
        v-model="PhoneNumber"
        label="Номер телефона"
        type="number"
        class="the-input"
        compulsory
        :show-compulsory-error-msg="showCompulsoryErrorMsg"
    />
    <div class="label">Пол</div>
    <div class="user-create-form__radio-group">
    <the-input
      v-model="male"
      label="Мужской"
      type="radio"
      class="the-input_type-radio"
      @input="female=false"
    />
    <the-input
      v-model="female"
      label="Женский"
      type="radio"
      class="the-input_type-radio"
      @input="male=false"
    />
    </div>
    <the-select
        v-model="ClientGroup"
        :options="[
        {label: 'VIP', value: 'VIPClients'},
        {label: 'Проблемные', value: 'ProblemClients'},
        {label: 'ОМС', value: 'OMSClients'}
        ]"
        placeholder="Выберите группу клиентов"
        multiselect
    />
    <the-select
        v-model="selectedDoctor"
        :options="[
            {label: 'Иванов', value: 'Ivanov'},
            {label: 'Захаров', value: 'Zakharov'},
            {label: 'Чернышева', value: 'Chernisheva'},
        ]"
        placeholder="Выберите врача"
        class="select"
    />

    <the-input
        v-model="Message"
        label="Не отправлять СМС"
        type="checkbox"
        class="the-input_type-radio"
    />
    <div class="label group-label">Адрес</div>
    <the-input
        v-model="ZipCode"
        label="Индекс"
        type="number"
        class="the-input"
    />
    <the-input
        v-model="Country"
        :invalid="textIsInvalid(Country)"
        label="Страна"
        type="text"
        class="the-input"
        error-msg="Название страны может содержать только буквы кириллицы и латинского алфавита и тире"
    />
    <the-input
        v-model="Area"
        :invalid="textIsInvalid(Area)"
        label="Область"
        type="text"
        class="the-input"
        error-msg="Название области может содержать только буквы кириллицы и латинского алфавита и тире"
    />
    <the-input
        v-model="City"
        label="Город"
        type="text"
        class="the-input"
    />
    <the-input
        v-model="Street"
        label="Улица"
        type="text"
        class="the-input"
    />
    <the-input
        v-model="House"
        label="Дом"
        type="text"
        class="the-input"
    />
    <div class="label group-label">Документ</div>
    <the-select
        v-model="selectedDocument"
        :options="[
            {label: 'Паспорт', value: 'passport'},
            {label: 'Свидетельство о рождении', value: 'birthСertificate'},
            {label: 'Водительское удостоверение', value: 'driverLicense'},
        ]"
        placeholder="Выберите тип документа"
        class="select"
        compulsory
        :show-compulsory-error-msg="showCompulsoryErrorMsg"
        />
    <the-input
        v-model="Series"
        label="Серия"
        type="number"
        class="the-input"
    />
    <the-input
        v-model="number"
        label="Номер"
        type="number"
        class="the-input"
    />
    <the-input
        v-model="GivenBy"
        label="Кем выдан"
        type="text"
        class="the-input"
    />
    <the-input
        v-model="DateGiven"
        label="Дата выдачи"
        type="date"
        class="the-input__type-date"
        compulsory
        :show-compulsory-error-msg="showCompulsoryErrorMsg"
    />
    <button class="user-create-form__button" @click="submit">Отправить форму</button>
    <the-alert
      v-if="alert.show"
      :text="alert.text"
      :variant="alert.variant"
      @hide="alert.show = false"
    />
  </div>
</template>

<script>
import TheInput from '@/components/TheInput.vue'
import TheSelector from '@/components/TheSelector.vue'
import TheSelect from "@/components/TheSelector.vue";
import TheAlert from "@/components/TheAlert.vue";
export default {
  name: "UserCreateForm",
  components: {
    TheAlert,
    TheSelect,
    TheInput,
    TheSelector
  },
  data() {
    return {
      LastName: "",
      Name: "",
      Patronymic: "",
      BirthDate: "",
      PhoneNumber: "",
      male: false,
      female: false,
      ZipCode: "",
      Country: "",
      Area: "",
      City: "",
      Street: "",
      House: "",
      Series: "",
      number: "",
      GivenBy: "",
      DateGiven: "",
      selectedDoctor: {label: "", value: ""},
      selectedDocument: {label: "", value: ""},
      selectedArr: [],
      Message: false,
      ClientGroup: [],
      showCompulsoryErrorMsg: false,
      alert: {show: false, text: "", variant: ""}
    }
  },
  computed: {
    CompulsoryFormsFilled(){
      return this.LastName !== "" && this.Name !== "" && this.BirthDate !== "" && this.PhoneNumber !== ""
          && this.ClientGroup.length !== 0 && this.selectedDoctor.value !== "" && this.selectedDocument.value !== "" && this.DateGiven !== ""
    },
  },
  methods: {
    textIsInvalid(text) {
      return !/^[A-Za-zА-Яа-я-]+$/.test(text) && text !== ''
    },
    AllFormsValid() {
      return !this.textIsInvalid(this.LastName) && !this.textIsInvalid(this.Name) && !this.textIsInvalid(this.Patronymic)
      && !this.textIsInvalid(this.Country) && !this.textIsInvalid(this.Area)
    },
    submit() {
      if (!this.CompulsoryFormsFilled) {
        this.showCompulsoryErrorMsg = true
        this.alert.show = true
        this.alert.text = "Заполните все обязательные поля"
        this.alert.variant = "fail"
        return
      }
      this.showCompulsoryErrorMsg = false
      console.log(!this.textIsInvalid(this.LastName),!this.textIsInvalid(this.Name), !this.textIsInvalid(this.Patronymic),
          !this.textIsInvalid(this.Country), !this.textIsInvalid(this.Area))
      console.log(this.AllFormsValid)
      if (!this.AllFormsValid()) {
        this.alert.show = true
        this.alert.text = "Не все поля верно заполнены"
        this.alert.variant = "fail"
        return
      }
      this.alert.show = true
      this.alert.text = "Успешно создан новый клиент"
      this.alert.variant = "success"
    }
  }
}
</script>

<style scoped>
.user-create-form{
  display: flex;
  flex-direction: column;
  padding: 75px 100px 75px 100px;
  background-color: aliceblue;
  font-size: 20px;
  @media screen and (max-width: 550px) {
    padding: 50px 30px 50px 30px;
  }
}


.the-input_type-radio{
  display: flex;
  flex-direction: row;
  margin-right: 7vw;
}

.the-input_type-radio[type="radio"]:after{
  color: #43799b;
}

.user-create-form__radio-group{
  margin-bottom: 20px;
  margin-top: 20px;
  display: flex;
  flex-direction: row;
  align-items: center;
  align-self: flex-start;
  justify-content: space-between;
}

.label{
  width: 100%;
  text-align: left;
  margin-top: 30px;
}

.group-label {
  margin-bottom: 15px;
  font-weight: bold;
  font-size: 1.2em;
}
.user-create-form__button{
  font-family: Rateway, serif;
  width: 40%;
  align-self: center;
  font-size: .9em;
  border: 1px solid #43799b;
  border-radius: 10px;
  background-color: #85c2e2;
}
.user-create-form__button:hover{
  background-color: #9bd9f8;
}
</style>