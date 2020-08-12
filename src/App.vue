<template>
  <div id="app">
    <div class="container">
      <form class="form" @submit.prevent="submitHandler()">
        <div class="title">Атрибуты формы:</div>

        <div class="form-block">
          <label class="label" :class="{ 'form-group--error': $v.formData.surname.$error }">
            <input
              type="text"
              class="input-text"
              placeholder="Фамилия*"
              v-model.trim="$v.formData.surname.$model"
            />
            <span class="input-error" v-if="$v.formData.surname.$error">Поле обязательно</span>
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Имя*"
              v-model.trim="$v.formData.name.$model"
            />
            <span class="input-error" v-if="$v.formData.name.$error">Поле обязательно</span>
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Отчество"
              v-model.trim="formData.patronymic"
            />
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Дата рождения*"
              v-model.trim="$v.formData.dateOfBirth.$model"
            />
            <span class="input-error" v-if="$v.formData.dateOfBirth.$error">Поле обязательно</span>
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Номер телефона*"
              v-model.trim="$v.formData.phone.$model"
            />
            <span class="input-error" v-if="$v.formData.phone.$error">Поле обязательно</span>
          </label>

          <label class="label">
            <select class="input-text" v-model="formData.gender">
              <option disabled value="">Пол</option>
              <option v-for="(item, index) in initData.gender" :key="index">{{ item }}</option>
            </select>
          </label>

          <label class="label">
            <select
              class="input-multiple"
              multiple
              size="3"
              v-model.trim="$v.formData.clientGroup.$model"
            >
              <option v-for="(item, index) in initData.clientGroup" :key="index">{{ item }}</option>
            </select>
            <span class="input-error" v-if="$v.formData.clientGroup.$error">
              Необходимо выбрать хотя бы один вариант
            </span>
          </label>

          <label class="label">
            <select class="input-text" v-model="formData.doctor">
              <option disabled value="">Лечащий врач</option>
              <option v-for="(item, index) in initData.doctor" :key="index">{{ item }}</option>
            </select>
          </label>

          <label class="label-chbox label">
            <input type="checkbox" v-model="formData.isSendSMS" />
            <span>Не отправлять СМС</span>
          </label>
        </div>

        <div class="title">Адрес:</div>

        <div class="form-block">
          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Индекс"
              v-model.trim="formData.postcode"
            />
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Страна"
              v-model.trim="formData.country"
            />
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Область"
              v-model.trim="formData.region"
            />
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Город*"
              v-model.trim="$v.formData.city.$model"
            />
            <span class="input-error" v-if="$v.formData.city.$error">Поле обязательно</span>
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Улица"
              v-model.trim="formData.street"
            />
          </label>

          <label class="label">
            <input type="text" class="input-text" placeholder="Дом" v-model.trim="formData.house" />
          </label>
        </div>

        <div class="title">Паспорт:</div>

        <div class="form-block">
          <label class="label">
            <select class="input-text" v-model.trim="$v.formData.documentType.$model">
              <option disabled value="">Тип документа*</option>
              <option v-for="(item, index) in initData.documentType" :key="index">{{
                item
              }}</option>
            </select>
            <span class="input-error" v-if="$v.formData.documentType.$error"
              >Необходимо выбрать вариант</span
            >
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Серия"
              v-model.trim="formData.series"
            />
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Номер"
              v-model.trim="formData.number"
            />
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Кем выдан"
              v-model.trim="formData.issuedBy"
            />
          </label>

          <label class="label">
            <input
              type="text"
              class="input-text"
              placeholder="Дата выдачи*"
              v-model.trim="$v.formData.dateOfIssue.$model"
            />
            <span class="input-error" v-if="$v.formData.dateOfIssue.$error">Поле обязательно</span>
          </label>
        </div>

        <button class="button">Создать</button>
      </form>
    </div>

    <Toast :text="'Новый клиент успешно создан'" ref="toast" />
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
import Toast from "@/components/Toast";

export default {
  name: "App",
  components: { Toast },
  data() {
    return {
      initData: {
        gender: ["Мужской", "Женский"],
        clientGroup: ["VIP", "Проблемные", "ОМС"],
        doctor: ["Иванов", "Захаров", "Чернышева"],
        documentType: ["Паспорт", "Свидетельство о рождении", "Вод. удостоверение"]
      },
      formData: {
        surname: "",
        name: "",
        patronymic: "",
        dateOfBirth: "",
        phone: "",
        gender: "",
        clientGroup: [],
        doctor: "",
        isSendSMS: false,
        postcode: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
        documentType: "",
        series: "",
        number: "",
        issuedBy: "",
        dateOfIssue: ""
      }
    };
  },
  validations: {
    formData: {
      surname: { required },
      name: { required },
      dateOfBirth: { required },
      phone: { required },
      clientGroup: { required },
      city: { required },
      documentType: { required },
      dateOfIssue: { required }
    }
  },
  methods: {
    submitHandler() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        this.$refs.toast.showHandler();

        console.log("-->", this.formData);

        this.formData = {
          surname: "",
          name: "",
          patronymic: "",
          dateOfBirth: "",
          phone: "",
          gender: "",
          clientGroup: [],
          doctor: "",
          isSendSMS: false,
          postcode: "",
          country: "",
          region: "",
          city: "",
          street: "",
          house: "",
          documentType: "",
          series: "",
          number: "",
          issuedBy: "",
          dateOfIssue: ""
        };

        this.$v.$reset();
      }
    }
  }
};
</script>

<style lang="sass">
@import 'assets/styles/main.sass'

#app
  padding: 50px 0
</style>
