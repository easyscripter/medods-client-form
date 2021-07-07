<template>
  <div id="app">
    <form class="form-container">
      <h2>Форма клиента</h2>
      <div class="form-group">
        <altero-field fieldName="Имя*:" v-model="name"></altero-field>
        <altero-field fieldName="Фамилия*:" v-model="surName"></altero-field>
      </div>
      <div class="form-group">
        <altero-field
          fieldName="Отчество*:"
          v-model="patronymic"
        ></altero-field>
      </div>
      <date-field fieldName="Дата Рождения*:" v-model="birthday"></date-field>
      <phone-field
        fieldName="Номер телефона*:"
        v-model="phoneNumber"
      ></phone-field>
      <div class="form-group">
        <easy-select
          :options="sex"
          @select="getOptionSex"
          :selected="selectedSex"
          fieldName="Пол:"
        ></easy-select>
        <easy-select
          :options="doctor"
          @select="getOption"
          :selected="selectedDoctor"
          fieldName="Лечащий Врач:"
        ></easy-select>
      </div>

      <!-- <easy-select-multiple
        fieldName="Укажите группу:"
        v-model="selectedClientGroup"
      >
        <option v-for="(item, index) in items" :key="index">{{ item }}</option>
      </easy-select-multiple> -->
      <h3 class="group-header">Адрес:</h3>
      <div class="form-group">
        <altero-field fieldName="Старна:" v-model="country"></altero-field>
      </div>
      <div class="form-group">
        <altero-field fieldName="Область:" v-model="region"></altero-field>
        <altero-field fieldName="Город*:" v-model="city"></altero-field>
      </div>
      <div class="form-group">
        <altero-field fieldName="Улица:" v-model="street"></altero-field>
      </div>
      <div class="form-group">
        <altero-field fieldName="Индекс:" v-model="postIndex"></altero-field>
        <altero-field fieldName="Дом:" v-model="house"></altero-field>
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
        <altero-field fieldName="Серия:" v-model="docSeries"></altero-field>
        <altero-field fieldName="Номер:" v-model="docNumber"></altero-field>
      </div>
      <div class="form-group">
        <altero-field
          fieldName="Кем выдан:"
          v-model="organization"
        ></altero-field>
      </div>
      <div class="form-group">
        <date-field fieldName="Дата Выдачи*:" v-model="docDate"></date-field>
      </div>
    </form>
  </div>
</template>

<script>
import AlteroField from "@/components/AlteroField";
import DateField from "@/components/DateField";
import PhoneField from "@/components/PhoneField";
import EasySelect from "@/components/EasySelect";
// import EasySelectMultiple from "@/components/EasySelectMultiple";
export default {
  name: "App",
  components: {
    AlteroField,
    DateField,
    PhoneField,
    EasySelect,
    // EasySelectMultiple,
  },
  data() {
    return {
      surName: "",
      name: "",
      patronymic: "",
      birthday: "",
      phoneNumber: "+7 (",
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
      items: ["VIP", "Проблемные", "ОМС"],
      selectedSex: "Мужской",
      selectedDoctor: "Иванов",
      selectedClientGroup: [],
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
    };
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
  width: 300px;
  margin: 30px auto;
  padding: 40px;
  border-radius: 10px;
  -webkit-box-shadow: 4px 4px 13px 1px rgba(34, 60, 80, 0.28);
  -moz-box-shadow: 4px 4px 13px 1px rgba(34, 60, 80, 0.28);
  box-shadow: 4px 4px 13px 1px rgba(34, 60, 80, 0.28);
}

.form-group {
  display: flex;
  justify-content: space-between;
}

.group-header {
  text-align: left;
  font-size: 18px;
  margin-top: 40px;
}
</style>
