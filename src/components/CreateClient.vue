<template>
  <div class="createClientForm">
    <div class="container">
      <form  @submit.prevent="submitData">
        <h2>Создание клиента</h2>
        <div class="client-info">
          <div class="client-info_one">
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.surname.$error ? 'red' : '' }" for="surname">Фамилия*</label>
                <template v-if="$v.createClient.surname.$error">
                  <span class="errorMsg" v-if="!$v.createClient.surname.required">{{ msgRequired }}</span>
                  <span class="errorMsg" v-if="!$v.createClient.surname.minLength">{{ msgMinLength }}</span>
                  <span class="errorMsg" v-if="!$v.createClient.surname.maxLength">{{ msgMaxLength }}</span>
                </template>                
              </div>
              <input type="text" v-model="createClient.surname" placeholder="Введите Фамилия" 
              @blur="$v.createClient.surname.$touch()" 
              :style="{ borderColor: $v.createClient.surname.$error ? 'red' : '' }"
              >
            </div>
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.name.$error ? 'red' : '' }" for="name">Имя*</label>
                <template v-if="$v.createClient.name.$error">
                  <span class="errorMsg" v-if="!$v.createClient.name.required">{{ msgRequired }}</span>
                  <span class="errorMsg" v-if="!$v.createClient.name.minLength">{{ msgMinLength }}</span>
                  <span class="errorMsg" v-if="!$v.createClient.name.maxLength">{{ msgMaxLength }}</span>
                </template>                
              </div>
              <input id="name" type="text" v-model="createClient.name" placeholder="Введите имя"
              @blur="$v.createClient.name.$touch()"
              :style="{ borderColor: $v.createClient.name.$error ? 'red' : '' }">
            </div>
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.patronymic.$error ? 'red' : '' }" for="patronymic">Отчество</label>
                <template v-if="$v.createClient.patronymic.$error">
                  <span class="errorMsg" v-if="!$v.createClient.patronymic.minLength">{{ msgMinLength }}</span>
                  <span class="errorMsg" v-if="!$v.createClient.patronymic.maxLength">{{ msgMaxLength }}</span>
                </template>                
              </div>
              <input id="patronymic" type="text" v-model="createClient.patronymic" placeholder="Введите имя" 
              @blur="$v.createClient.patronymic.$touch()"
              :style="{ borderColor: $v.createClient.patronymic.$error ? 'red' : '' }">
            </div>
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.DateOfBirth.$error ? 'red' : '' }" for="DateOfBirth">Дата рождения*</label>
                <template v-if="$v.createClient.DateOfBirth.$error">
                  <span class="errorMsg" v-if="!$v.createClient.DateOfBirth.required">{{ msgRequired }}</span>
                </template>                
              </div>
              <input id="DateOfBirth" type="date" v-model="createClient.DateOfBirth" placeholder="Введите имя" 
              @blur="$v.createClient.DateOfBirth.$touch()"
              :style="{ borderColor: $v.createClient.DateOfBirth.$error ? 'red' : '' }">
            </div>

            <div class="sms-checkbox">
              <input class="checkbox" type="checkbox" id="smsCheckbox" v-model="createClient.sendSMS">
              <span>Не отправлять SMS</span>
            </div>
          </div>

          <div class="client-info_two">
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.phone_number.$error ? 'red' : '' }"  for="phone_number">Номер телефона*</label>
                <template v-if="$v.createClient.phone_number.$error">
                  <span class="errorMsg" v-if="!$v.createClient.phone_number.required">{{ msgRequired }}</span>
                  <span class="errorMsg" v-else-if="!$v.createClient.phone_number.validatePhone">Неправильный номер</span>
                </template>
              </div>
              <input id="phone_number" type="text" v-model="createClient.phone_number" placeholder="+7 (___) ___-__-__" 
              @blur="$v.createClient.phone_number.$touch()"
              :style="{ borderColor: $v.createClient.phone_number.$error ? 'red' : '' }">
            </div>
            <div class="field">
              <label for="gender">Выберите пол:</label>
              <select v-model="createClient.gender" id="gender">
                <option value="">Не указано</option>
                <option value="male">Мужской</option>
                <option value="female">Женский</option>
                <option value="other">Другой</option>
              </select>
            </div>
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.selectedGroups.$error ? 'red' : '' }" for="selectedGroups">Группа клиентов*</label>
                <template v-if="$v.createClient.selectedGroups.$error">
                  <span class="errorMsg" v-if="!$v.createClient.selectedGroups.required">{{ msgRequired }}</span>
                </template>
              </div>
              <select :style="{ borderColor: $v.createClient.selectedGroups.$error ? 'red' : '' }" 
              @blur="$v.createClient.selectedGroups.$touch()" v-model="createClient.selectedGroups" 
              name="" id="selectedGroups" multiple>
                <option value="VIP">VIP</option>
                <option value="Проблемные">Проблемные</option>
                <option value="ОМС">ОМС</option>
              </select>
            </div>
            <div class="field">
              <label for="doctor">Лечащий врач:</label>
              <select v-model="createClient.doctor" id="doctor">
                <option value="">Не указано</option>
                <option value="Иванов">Иванов</option>
                <option value="Захаров">Захаров</option>
                <option value="Чернышева">Чернышева</option>
              </select>
            </div>
          </div>
        </div>

        <div class="client-addres">
          <div class="client-addres_one">
            <div class="field">
              <label for="name">Индекс</label>
              <input id="name" type="text" v-model="createClient.index" placeholder="Введите Адрес" @blur="$v.createClient.index.$touch()">
            </div>
            <div class="field">
              <label for="country">Страна</label>
              <select v-model="createClient.country" id="country" placeholder="Выберите страну" >
                <option value="">Не указано</option>
                <option value="Россия">Россия</option>
                <option value="Украина">Украина</option>
                <option value="Казахстан">Казахстан</option>
                <option value="Беларуссия">Беларуссия</option>
              </select>
            </div>
            <div class="field">
              <label for="name">Область</label>
              <input id="name" type="text" v-model="createClient.region" placeholder="Введите Область" @blur="$v.createClient.region.$touch()">
            </div>
          </div>
          <div class="client-addres_two">
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.city.$error ? 'red' : '' }" for="name">Город*</label>
                <template v-if="$v.createClient.city.$error">
                  <span class="errorMsg" v-if="!$v.createClient.city.required">{{ msgRequired }}</span>
                </template>
              </div>
              <input 
              :style="{ borderColor: $v.createClient.city.$error ? 'red' : '' }" 
              id="name" type="text" v-model="createClient.city" placeholder="Введите Город" 
              @blur="$v.createClient.city.$touch()">
            </div>
            <div class="field">
              <label for="name">Улица</label>
              <input id="name" type="text" v-model="createClient.name" placeholder="Введите Улицу" @blur="$v.createClient.name.$touch()">
            </div>
            <div class="field">
              <label for="name">Дом</label>
              <input id="name" type="text" v-model="createClient.name" placeholder="Введите Дом" @blur="$v.createClient.name.$touch()">
            </div>
          </div>
        </div>
        
        <div class="client-passport">
          <div class="client-passport_one">
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.typeOfDocument.$error ? 'red' : '' }" for="typeOfDocument">Тип документа*</label>
                <template v-if="$v.createClient.typeOfDocument.$error">
                  <span v-if="!$v.createClient.typeOfDocument.required" class="errorMsg">{{ msgRequired }}</span>
                </template>
              </div>
              <select @blur="$v.createClient.typeOfDocument.$touch()" placeholder="выберите тим документа"
               v-model="createClient.typeOfDocument" id="typeOfDocument"
               :style="{ borderColor: $v.createClient.typeOfDocument.$error ? 'red' : '' }">
                <option value="male">Паспорт</option>
                <option value="female">Свидетельство о рождения</option>
                <option value="other">Вод.удостоверение</option>
              </select>
            </div>
            <div class="field">
              <label for="name">Серия</label>
              <input id="name" type="text" v-model="createClient.passport_series" placeholder="Введите Серию" @blur="$v.createClient.name.$touch()">
            </div>
          </div>
          <div class="client-passport_one">
            <div class="field">
              <label for="name">Номер</label>
              <input id="name" type="text" v-model="createClient.passport_number" placeholder="Введите Номер" @blur="$v.createClient.name.$touch()">
            </div>
            <div class="field">
              <label for="name">Кем выдан</label>
              <input id="name" type="text" v-model="createClient.issuedByWhom" placeholder="Введите кем выдан" @blur="$v.createClient.name.$touch()">
            </div>
            <div class="field">
              <div class="error">
                <label :style="{ color: $v.createClient.dateOfIssue.$error ? 'red' : '' }"  for="dateOfIssue">Дата выдачи*</label>
                <template v-if="$v.createClient.dateOfIssue.$error">
                  <p class="errorMsg" v-if="!$v.createClient.dateOfIssue.required">{{ msgRequired }}</p>
                </template>
              </div>
              <input id="dateOfIssue" type="date" v-model="createClient.dateOfIssue" 
              placeholder="Введите имя" @blur="$v.createClient.dateOfIssue.$touch()"
              :style="{ borderColor: $v.createClient.dateOfIssue.$error ? 'red' : '' }">
            </div>
          </div>
        </div>

        <div class="submit">
          <button >Подтвердить</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
  import { required , minLength, maxLength} from 'vuelidate/lib/validators'
  export default {
    name: 'CreateClientForm',
    data(){
      return {
        msgRequired: 'Поле обязательное',
        msgMinLength: 'не меньше 2 симв.',
        msgMaxLength: 'не больше 20 симв.',
        createClient: {
          surname: '',
          name: '',
          patronymic: '',
          DateOfBirth: '',
          phone_number: '+7',
          gender: '',
          selectedGroups: [],
          doctor: '',
          sendSMS: false,

          index: '',
          country: '',
          region: '',
          city: '',
          street: '',
          house: '',

          typeOfDocument: '',
          passport_series: '',
          passport_number: '',
          issuedByWhom: '',
          dateOfIssue: '',
        },
        feedback: ''
      }
    },
    methods: {
      submitData() {
        if(this.$v.$invalid){
          this.$v.$touch()
          return
        }
        else{
          alert('Вы успешно заполнили форму:)')
        }

      }
    },
    validations: {
      createClient: {
        surname: {
          required,
          minLength: minLength(2),
          maxLength: maxLength(20)
        },
        name: {
          required,
          minLength: minLength(2),
          maxLength: maxLength(20)
        },
        patronymic: {
          minLength: minLength(2),
          maxLength: maxLength(20)
        },
        DateOfBirth: {
          required
        },
        phone_number: {
          required,
          validatePhone(value) {
            const num = value.trim()
            return /^((\+7|7|8)+([0-9]){10})$/.test(num)
          }
        },
        selectedGroups: {
          required,
        },
        city: {
          required,
        },

        typeOfDocument: {
          required
        },
        dateOfIssue: {
          required
        }

      }
    }
  }
</script>

<style lang="sass">
 * 
  box-sizing: border-box
  margin: 0
  padding: 0
  font-family: 'Franklin Gothic Medium', sans-serif
form 
  display: flex
  flex-direction: column
  gap: 30px
  height: auto

.container 
  max-width: 600px
  width: 100%

.createClientForm 
  display: flex
  justify-content: center
  margin-top: 30px

.field 
  max-width: 260px
  height: 30px

.client-info, .client-addres, .client-passport 
  display: flex
  gap: 100px

input, select 
  width: 100%
  height: 100%
  padding: 0 5px
  border-radius: 4px
  border: 1px solid #cccccc
  margin-top: 5px

.sms-checkbox, .checkbox 
  display: flex
  align-items: flex-end
  gap: 5px

.checkbox
  width: 16px  
.error 
  display: flex
  align-items: flex-end

.errorMsg 
  font-size: 11px
  color: red

.client-info_one, .client-info_two, .client-addres_one, .client-addres_two, .client-passport_one, .client-passport_two 
  display: flex
  flex-direction: column
  gap: 30px
  width: 100%

button 
  max-height: 40px
  background-color: #0c5c48
  color: white
  width: 100%
  padding: 5px
  border: 1px solid #0c5c48
  border-radius: 2px
  cursor: pointer
  transition: background-color 0.3s

  &:hover
    background-color: #0a4038

  &:disabled
    background-color: #ccc
    color: #666
    cursor: not-allowed
    border: 1px solid #ccc

.submit 
  margin-top: 20px


     
</style>


