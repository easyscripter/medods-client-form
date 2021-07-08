<template>
  <div id="app">
    <form class="form-container">
      <h2>Форма клиента</h2>
      <div class="form-group">
        <div class="input-group">
          <altero-field
            fieldName="Имя*:"
            v-model.trim="$v.name.$model"
          ></altero-field>
          <div class="error" v-if="!$v.name.minLength">
            Имя должно быть больше {{ $v.name.$params.minLength.min }} символов
          </div>
          <div class="error" v-else-if="!$v.name.required">
            Вы не указали Имя
          </div>
          <div class="error" v-else-if="!$v.name.checkStringRule">
            Имя должно быть строкой
          </div>
        </div>
        <div class="input-group">
          <altero-field
            fieldName="Фамилия*:"
            v-model.trim="$v.surName.$model"
          ></altero-field>
          <div class="error" v-if="!$v.surName.minLength">
            Фамилия должна быть больше
            {{ $v.surName.$params.minLength.min }} символов
          </div>
          <div class="error" v-else-if="!$v.surName.required">
            Вы не указали Фамилию
          </div>
          <div class="error" v-else-if="!$v.name.checkStringRule">
            Фамилия должна быть строкой
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="input-group">
          <altero-field
            fieldName="Отчество*:"
            v-model.trim="$v.patronymic.$model"
          ></altero-field>
          <div class="error" v-if="!$v.surName.minLength">
            Отчество должно быть больше
            {{ $v.patronymic.$params.minLength.min }} символов
          </div>
          <div class="error" v-else-if="!$v.patronymic.required">
            Вы не указали Отчество
          </div>
          <div class="error" v-else-if="!$v.patronymic.checkStringRule">
            Отчество должно быть строкой
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="input-group">
          <date-field
            fieldName="Дата Рождения*:"
            v-model.trim="$v.birthday.$model"
          ></date-field>
          <div class="error" v-if="!$v.birthday.required">
            Вы не указали дату рождения
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="input-group">
          <phone-field
            fieldName="Номер телефона*:"
            v-model.trim="$v.phoneNumber.$model"
          ></phone-field>
          <div class="error" v-if="!$v.phoneNumber.minLength">
            Номер телефона должен быть больше 11 символов
          </div>
        </div>
      </div>
      <div class="form-group">
        <easy-select
          :options="sex"
          @select="getOptionSex"
          :selected="selectedSex"
          fieldName="Пол:"
        ></easy-select>
        <easy-select
          :options="doctor"
          @select="getOptionDoc"
          :selected="selectedDoctor"
          fieldName="Лечащий Врач:"
        ></easy-select>
      </div>
      <div class="form-group">
        <div class="input-group">
          <easy-select-multiple
            fieldName="Выберите группу клиентов*:"
            :items="clientGroups"
            @getValues="getClientGroups"
          ></easy-select-multiple>
          <div class="error" v-if="selectedClientGroups.length < 1">
            Вы не выбрали группу клиентов
          </div>
        </div>
      </div>
      <div class="form-group sms-checkbox">
        <input v-model="isSendSMS" type="checkbox" id="checkbox-sms" />
        <label for="checkbox-sms">Отправить смс</label>
      </div>
      <h3 class="group-header">Адрес:</h3>
      <div class="form-group">
        <div class="input-group">
          <altero-field
            fieldName="Страна:"
            v-model="$v.country.$model"
          ></altero-field>
          <div class="error" v-if="!$v.country.checkStringRule">
            Страна должна быть строкой
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="input-group">
          <altero-field
            fieldName="Область:"
            v-model="$v.region.$model"
          ></altero-field>
          <div class="error" v-if="!$v.region.checkStringRule">
            Регион должен быть строкой
          </div>
        </div>
        <div class="input-group">
          <altero-field fieldName="Город*:" v-model="city"></altero-field>
          <div class="error" v-if="!$v.city.minLength">
            Город должна быть больше
            {{ $v.city.$params.minLength.min }} символов
          </div>
          <div class="error" v-else-if="!$v.city.required">
            Вы не указали Город
          </div>
          <div class="error" v-else-if="!$v.city.checkStringRule">
            Город должен быть строкой
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="input-group">
          <altero-field
            fieldName="Улица:"
            v-model="$v.street.$model"
          ></altero-field>
          <div class="error" v-if="!$v.street.checkStringRule">
            Улица должна быть строкой
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="input-group">
          <altero-field
            fieldName="Индекс:"
            v-model.number="$v.postIndex.$model"
          ></altero-field>
          <div class="error" v-if="!$v.postIndex.checkNumberRule">
            Индекс должен быть числом
          </div>
        </div>
        <div class="input-group">
          <altero-field fieldName="Дом:" v-model="house"></altero-field>
        </div>
      </div>
      <h3 class="group-header">Паспортные данные:</h3>
      <div class="form-group">
        <easy-select
          :options="typeOfDocuments"
          @select="getOptionDoc"
          :selected="selectedTypeOfDoc"
          fieldName="Тип документа*:"
        ></easy-select>
      </div>
      <div class="form-group">
        <div class="input-group">
          <altero-field
            fieldName="Серия:"
            v-model.number="$v.docSeries.$model"
          ></altero-field>
          <div class="error" v-if="!$v.docSeries.checkNumberRule">
            Серия должна быть числом
          </div>
        </div>
        <div class="input-group">
          <altero-field
            fieldName="Серия:"
            v-model.number="$v.docNumber.$model"
          ></altero-field>
          <div class="error" v-if="!$v.docNumber.checkNumberRule">
            Номер должен быть числом
          </div>
        </div>
      </div>
      <div class="form-group">
        <altero-field
          fieldName="Кем выдан:"
          v-model="organization"
        ></altero-field>
      </div>
      <div class="form-group">
        <div class="input-group">
          <date-field
            fieldName="Дата Выдачи*:"
            v-model="$v.docDate.$model"
          ></date-field>
          <div class="error" v-if="!$v.docDate.required">
            Вы не указали дату выдачи документа
          </div>
        </div>
      </div>
      <altero-button
        bgColor="white"
        buttonText="Отправить анекту"
        @clickOnButton="handleQuestionnaire"
      ></altero-button>
      <p class="success" v-if="formIsValid">Анекта успешно отправлена</p>
    </form>
  </div>
</template>

<script>
import AlteroField from "@/components/AlteroField";
import AlteroButton from "@/components/AlteroButton";
import DateField from "@/components/DateField";
import PhoneField from "@/components/PhoneField";
import EasySelect from "@/components/EasySelect";
import EasySelectMultiple from "@/components/EasySelectMultiple";
import { required, minLength } from "vuelidate/lib/validators";

const checkStringRule = (value) => typeof value == "string";
const checkNumberRule = (value) => typeof value == "number";

export default {
  name: "App",
  components: {
    AlteroField,
    DateField,
    PhoneField,
    EasySelect,
    EasySelectMultiple,
    AlteroButton,
  },
  data() {
    return {
      surName: "",
      name: "",
      patronymic: "",
      birthday: "",
      phoneNumber: "+7",
      sex: [
        { value: "Мужской", name: "Мужской" },
        { value: "Женский", name: "Женский" },
      ],
      doctor: [
        { value: "Иванов", name: "Иванов" },
        { value: "Захаров", name: "Захаров" },
        { value: "Чернышева", name: "Чернышева" },
      ],
      typeOfDocuments: [
        { value: "Паспорт", name: "Паспорт" },
        { value: "Свидетельство о рождении", name: "Свидетельство о рождении" },
        { value: "Вод. Удостоверение", name: "Вод. Удостоверение" },
      ],
      clientGroups: ["VIP", "Проблемные", "ОМС"],
      selectedSex: "Мужской",
      selectedDoctor: "Иванов",
      selectedClientGroups: [],
      selectedTypeOfDoc: "Паспорт",
      country: "",
      region: "",
      city: "",
      street: "",
      postIndex: "",
      house: "",
      docSeries: "",
      docNumber: "",
      organization: "",
      docDate: "",
      isSendSMS: true,
      formIsValid: false,
    };
  },
  validations: {
    name: {
      required,
      minLength: minLength(2),
      checkStringRule,
    },
    surName: {
      required,
      minLength: minLength(2),
      checkStringRule,
    },
    patronymic: {
      required,
      minLength: minLength(2),
      checkStringRule,
    },
    birthday: {
      required,
    },
    phoneNumber: {
      required,
      minLength: minLength(12),
    },
    city: {
      required,
      minLength: minLength(3),
      checkStringRule,
    },
    country: {
      checkStringRule,
    },
    street: {
      checkStringRule,
    },
    region: {
      checkStringRule,
    },
    postIndex: {
      checkNumberRule,
    },
    docSeries: {
      checkNumberRule,
    },
    docNumber: {
      checkNumberRule,
    },
    docDate: {
      required,
    },
  },
  methods: {
    getOptionSex(option) {
      this.selectedSex = option.name;
    },
    getOptionDoctor(option) {
      this.selectedDoctor = option.name;
    },
    getOptionDoc(option) {
      this.selectedTypeOfDoc = option.name;
    },
    getClientGroups(items) {
      this.selectedClientGroups = items;
    },
    handleQuestionnaire() {
      const isGoodCommonsFields =
        this.$v.name.required &&
        this.$v.name.minLength &&
        this.$v.name.checkStringRule &&
        this.$v.surName.required &&
        this.$v.surName.minLength &&
        this.$v.surName.checkStringRule &&
        this.$v.patronymic.checkStringRule &&
        this.$v.patronymic.required &&
        this.$v.patronymic.minLength &&
        this.$v.birthday.required &&
        this.$v.phoneNumber.minLength &&
        this.$v.phoneNumber.required &&
        this.selectedClientGroups.length >= 1;

      let isGoodAddressFields =
        this.$v.city.required &&
        this.$v.city.minLength &&
        this.$v.city.checkStringRule;

      let isGoodDocFields = this.$v.docDate.required;

      if (isGoodCommonsFields && isGoodAddressFields && isGoodDocFields) {
        this.formIsValid = true;
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.form-container {
  max-width: 600px;
  margin: 30px auto;
  padding: 30px;
  border-radius: 10px;
  -webkit-box-shadow: 4px 4px 13px 1px rgba(34, 60, 80, 0.28);
  -moz-box-shadow: 4px 4px 13px 1px rgba(34, 60, 80, 0.28);
  box-shadow: 4px 4px 13px 1px rgba(34, 60, 80, 0.28);
}

.form-group {
  display: flex;
}
.input-group {
  width: 100%;
  margin-right: 15px;
}
.group-header {
  text-align: left;
  font-size: 18px;
  margin-top: 40px;
}
.sms-checkbox {
  margin-top: 20px;
}
.error {
  color: red;
  text-align: left;
}
.success {
  color: green;
  font-weight: bold;
}
</style>
