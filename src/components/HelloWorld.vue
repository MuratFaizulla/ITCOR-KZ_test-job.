<template>
  <div class="form-dialog">
    <div class="form-header">
      <button class="close-button" @click="closeForm">X</button>
    </div>
    <form @submit.prevent="submitForm">
      <div class="form-fields">
        <!-- Первый столбец -->
        <div class="column">
          <!-- Блок загрузки фото -->
          <div class="upload-container">
            <div class="upload-icon">
              <img :src="imageSrc" alt="">
            </div>
            <input type="file" id="file-input" class="upload-input" @change="handleFileUpload">
            <label for="file-input" class="upload-button">Загрузить фото</label>
          </div>
          <!-- Дополнительные поля аналогичным образом -->
          <div class="form-group">
            <label for="individual-number">Индивидуальный номер животного</label>
            <input type="text" id="individual-number" v-model="formData.individualNumber">
          </div>
          <!-- Поля с методами мечения -->
          <div class="form-group">
            <label>Метод мечения:</label>
            <div class="marking-method">
              <label><input type="checkbox" v-model="formData.markingMethods" value="bracelet"> Браслет</label>
              <label><input type="checkbox" v-model="formData.markingMethods" value="harness"> Шлейка</label>
              <label><input type="checkbox" v-model="formData.markingMethods" value="branding"> Клеймо</label>
              <label><input type="checkbox" v-model="formData.markingMethods" value="collar"> Ошейник</label>
              <label><input type="checkbox" v-model="formData.markingMethods" value="tag"> Бирка</label>
              <label><input type="checkbox" v-model="formData.markingMethods" value="chip"> Чип</label>
            </div>
          </div>
          <div class="form-group">
            <input type="text" placeholder="Идентификатор прибора учета" v-model="formData.deviceId">
          </div>
          <div class="form-group">
            <input type="text" placeholder="Кличка" v-model="formData.nickname">
          </div>
        </div>

        <!-- Второй столбец -->
        <div class="column">
          <!-- Ввод данных -->
          <div class="form-group">
            <label for="animal-type">Вид животного</label>
            <select id="animal-type" v-model="formData.animalType">
              <option value="">Выберите вид</option>
              <!-- Добавьте варианты видов здесь -->
            </select>
          </div>
          <div class="form-group">
            <select id="animal-breed" v-model="formData.animalBreed">
              <option value="">Порода животного</option>
              <!-- Добавьте варианты пород здесь -->
              <option value="breed1">1</option>
              <option value="breed2">2</option>
            </select>
          </div>
          <div class="form-group">
            <label for="animal-address">Адрес животного:</label>
            <input type="text" id="animal-address" placeholder="Область" v-model="formData.addressRegion">
          </div>
          <div class="form-group">
            <input type="text" placeholder="Район" v-model="formData.addressDistrict">
          </div>
          <div class="form-group">
            <input type="text" placeholder="Населенный пункт" v-model="formData.addressSettlement">
          </div>
          <!-- Переключатель Бродячее/Домашнее -->
          <div class="form-group">
            <label>Бродячее/домашнее:</label>
            <label class="switch">
              <input type="checkbox" v-model="formData.isStray">
              <span class="slider"></span>
            </label>
          </div>
          <div class="form-group">
            <label for="inn">ИНН</label>
            <input type="text" id="inn" v-model="formData.inn">
          </div>
          <div class="form-group">
            <label for="registration-date">Дата регистрации</label>
            <input type="date" id="registration-date" v-model="formData.registrationDate" class="date-input">
          </div>



        </div>

        <!-- Третий столбец -->
        <div class="column">
          <div class="form-group">
            <label for="weight">Характеристики животного</label>
            <input type="number" placeholder="Масса животного (гр)" id="weight" v-model="formData.weight">
          </div>
          <div class="form-group">
            <input type="number" placeholder="Высота животного в холке (мм)" id="height" v-model="formData.height">
          </div>
          <div class="form-group">
            <label for="age">Возраст животного</label>
            <div class="age-group">
              <label><input type="number" id="age-years" v-model="formData.ageYears" placeholder="0" min="0">
                Лет</label>
              <label><input type="number" id="age-months" v-model="formData.ageMonths" placeholder="0" min="0" max="11">
                Мес. </label>
            </div>
          </div>
          <div class="form-group">
            <label for="special-signs">Особые приметы</label>
            <textarea id="special-signs" v-model="formData.specialSigns"></textarea>
          </div>
          <div class="form-group">
            <label for="additional-info">Иные сведения</label>
            <textarea id="additional-info" v-model="formData.additionalInfo"></textarea>
          </div>
        </div>
      </div>

      <!-- Кнопки действий -->
      <div class="form-actions">
        <button type="button" class="cancel-button" @click="closeForm">Закрыть</button>
        <button type="submit" class="submit-button">Готово</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        individualNumber: '',
        markingMethods: [],
        deviceId: '',
        nickname: '',
        animalType: '',
        animalBreed: '',
        addressRegion: '',
        addressDistrict: '',
        addressSettlement: '',
        isStray: false,
        inn: '',
        registrationDate: '',
        weight: '',
        height: '',
        ageYears: '',
        ageMonths: '',
        specialSigns: '',
        additionalInfo: '',
      },
      imageSrc: 'logo.png',
    };
  },
  methods: {
    closeForm() {
    },
    submitForm() {
      console.log(this.formData);
    },
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        this.imageSrc = URL.createObjectURL(file);
      }
    },
  },
};
</script>

<style scoped>
.form-dialog {
  width: 1130px;
  height: 720px;
  margin-left: 150px;
  background-color: white;
  border-radius: 20px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
  font-family: Roboto, sans-serif;
  font-size: 16px;
  position: relative;
  padding: 75px 46px 0 46px;

}

.form-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.close-button {
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
  position: absolute;
  top: 15px;
  right: 15px;
}

.upload-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.upload-icon {
  width: 180px;
  height: 180px;
  background-color: #e5e5e5;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
}

.upload-icon img {
  width: 180px;
  height: 180px;
  border-radius: 50%;

}

.upload-button {
  width: 161px;
  margin-top: 24px;
  margin-bottom: 47px;
  padding: 12px 22px;
  border: 2px solid #ffb74d;
  border-radius: 15px;
  background-color: transparent;
  color: #D9940F;
  font-size: 16px;
  cursor: pointer;
  outline: none;
  display: flex;
  align-items: center;
  justify-content: center;
}

.upload-button:hover {
  background-color: #D9940F;
  color: white;
}

.upload-input {
  display: none;
}


.form-fields {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.column {
  flex: 1;
}

.form-group {
  margin-bottom: 15px;

}

.marking-method {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.marking-method label {
  flex-basis: calc(33.33% - 10px);
  display: flex;
  align-items: center;
}

input[type="checkbox"] {
  width: 24px;
  height: 24px;
  padding: 12px 15px;
  border: 1px solid #ccc;
  border-radius: 12px;
  font-size: 16px;
  box-sizing: border-box;
}

input[type="text"]:disabled {
  background-color: #f0f0f0;
  color: #aaa;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input,
select,
textarea {
  width: 330px;
  height: 48px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 15px;
  box-sizing: border-box;
}

select {
  padding: 10px 40px 10px 15px;
  border: 1px solid #ccc;
  border-radius: 12px;
  background-color: #fff;
  appearance: none;
  background-image: url('data:image/svg+xml;charset=US-ASCII,<svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="%23ccc" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 12 15 18 9"></polyline></svg>');
  /* Стрелка */
  background-repeat: no-repeat;
  background-position: calc(100% - 10px) center;
  background-size: 14px;
  cursor: pointer;
  box-sizing: border-box;
  color: #aaa;

}

textarea {
  height: 100px;
  resize: none;
}

.age-group {
  display: flex;
  gap: 50px;
}

.age-group input[type="number"] {
  width: 100px;
  border: 1px solid #ccc;
  border-radius: 15px;
  font-size: 16px;
}

.switch {
  position: relative;
  display: inline-block;
  width: 34px;
  height: 20px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  border-radius: 20px;
  width: 64px;
  height: 32px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 30px;
  width: 30px;
  border-radius: 50%;
  left: 1px;
  bottom: 1px;
  background-color: white;
  transition: 0.4s;
}

input:checked+.slider {
  background-color: #D9940F;
}

input:checked+.slider:before {
  transform: translateX(32px);
}


.form-actions {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
  margin-top: 20px;
}

.cancel-button,
.submit-button {
  padding: 12px 22px;
  border: none;
  border-radius: 15px;
  cursor: pointer;
}

.cancel-button {
  border: solid 2px #D9940F;
  background-color: #fff;
  color: #D9940F;
}

.submit-button {
  background-color: #D9940F;
  color: white;
}



input[type="date"] {
  border: 1px solid #dcdcdc;
  font-size: 14px;
  background-color: #ffffff;
  cursor: pointer;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  position: relative;
}

input[type="date"]::-webkit-calendar-picker-indicator {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  opacity: 0;
}



input[type="date"]::after {
  content: "▾";
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  pointer-events: none;
  font-size: 12px;
}
</style>
