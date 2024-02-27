<template>
  <div id="app">
    <div class="container">
      <form
        class="form"
        @submit.prevent="onSubmit"
      >
        <div class="client-reg-form">
          <h2 class="heading">Личные данные</h2>
          <div class="form-group">
            <label
              for="lastName"
              class="form-label"
              >Фамилия <span class="required">*</span></label
            >
            <input
              type="text"
              v-model.trim="$v.clientRegForm.lastName.$model"
              @blur="$v.clientRegForm.lastName.$touch()"
              maxlength="20"
              class="form-input"
              :class="{ 'form-input_error': $v.clientRegForm.lastName.$error }"
              id="lastName"
              placeholder="Введите фамилию"
            />
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.lastName.$dirty &&
                !$v.clientRegForm.lastName.required
              "
            >
              Поле обязательно для заполнения
            </div>
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.lastName.$dirty &&
                !$v.clientRegForm.lastName.minLength
              "
            >
              {{
                `Поле должно содержать минимум ${$v.clientRegForm.lastName.$params.minLength.min} буквы`
              }}
            </div>
          </div>
          <div class="form-group">
            <label
              for="firstName"
              class="form-label"
              >Имя <span class="required">*</span></label
            >
            <input
              type="text"
              v-model.trim="$v.clientRegForm.firstName.$model"
              @blur="$v.clientRegForm.firstName.$touch()"
              maxlength="20"
              class="form-input"
              :class="{ 'form-input_error': $v.clientRegForm.firstName.$error }"
              id="firstName"
              placeholder="Введите имя"
            />
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.firstName.$dirty &&
                !$v.clientRegForm.firstName.required
              "
            >
              Поле обязательно для заполнения
            </div>
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.firstName.$dirty &&
                !$v.clientRegForm.firstName.minLength
              "
            >
              {{
                `Поле должно содержать минимум ${$v.clientRegForm.firstName.$params.minLength.min} буквы`
              }}
            </div>
          </div>
          <div class="form-group">
            <label
              for="middleName"
              class="form-label"
              >Отчество</label
            >
            <input
              type="text"
              v-model.trim="$v.clientRegForm.middleName.$model"
              @blur="$v.clientRegForm.middleName.$touch()"
              class="form-input"
              :class="{
                'form-input_error': $v.clientRegForm.middleName.$error,
              }"
              id="middleName"
              placeholder="Введите отчество"
            />
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.middleName.$dirty &&
                !$v.clientRegForm.middleName.minLength
              "
            >
              {{
                `Поле должно содержать минимум ${$v.clientRegForm.middleName.$params.minLength.min} буквы`
              }}
            </div>
          </div>
          <div class="form-group">
            <label
              for="day"
              class="form-label"
              >Дата рождения <span class="required">*</span></label
            >
            <div class="birthday-input">
              <input
                type="tel"
                class="form-input birthday-number"
                v-model.trim="$v.clientRegForm.day.$model"
                @blur="$v.clientRegForm.day.$touch()"
                @input="onlyNumbers"
                :class="{
                  'form-input_error': $v.clientRegForm.day.$error,
                }"
                id="day"
                maxlength="2"
                autocomplete="off"
                spellcheck="false"
                placeholder="День"
              />
              <select
                name="month-select"
                class="form-select month-select"
                id="month"
                v-model.trim="$v.clientRegForm.month.$model"
                @blur="$v.clientRegForm.month.$touch()"
                :class="{
                  'form-input_error': $v.clientRegForm.month.$error,
                }"
              >
                <option
                  value=""
                  selected
                  disabled
                >
                  Месяц
                </option>
                <option value="1">Январь</option>
                <option value="2">Февраль</option>
                <option value="3">Март</option>
                <option value="4">Апрель</option>
                <option value="5">Май</option>
                <option value="6">Июнь</option>
                <option value="7">Июль</option>
                <option value="8">Август</option>
                <option value="9">Сентябрь</option>
                <option value="10">Октябрь</option>
                <option value="11">Ноябрь</option>
                <option value="12">Декабрь</option>
              </select>
              <input
                type="tel"
                class="form-input birthday-number"
                v-model.trim="$v.clientRegForm.year.$model"
                @blur="$v.clientRegForm.year.$touch()"
                @input="onlyNumbers"
                :class="{
                  'form-input_error': $v.clientRegForm.year.$error,
                }"
                name="year"
                maxlength="4"
                autocomplete="off"
                id="year"
                placeholder="Год"
              />
            </div>
            <div
              class="form_error"
              v-if="
                ($v.clientRegForm.day.$dirty &&
                  (!$v.clientRegForm.day.required ||
                    $v.clientRegForm.day.$error)) ||
                ($v.clientRegForm.month.$dirty &&
                  (!$v.clientRegForm.month.required ||
                    $v.clientRegForm.month.$error)) ||
                ($v.clientRegForm.year.$dirty &&
                  (!$v.clientRegForm.year.required ||
                    $v.clientRegForm.year.$error))
              "
            >
              Укажите дату рождения полностью
            </div>
          </div>
          <div class="form-group tel-group">
            <label
              for="tel"
              class="form-label"
              >Номер телефона <span class="required">*</span></label
            >

            <input
              type="tel"
              name="tel-input"
              id="tel"
              class="form-input tel-input"
              autocomplete="off"
              maxlength="17"
              placeholder="(___) ___-____"
              v-model="$v.clientRegForm.phoneNumber.$model"
              @input="telMask"
              @blur="$v.clientRegForm.phoneNumber.$touch()"
              :class="{
                'form-input_error': $v.clientRegForm.phoneNumber.$error,
              }"
            />
            <div class="num-prefix">+7</div>
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.phoneNumber.$dirty &&
                !$v.clientRegForm.phoneNumber.minLength
              "
            >
              Укажите номер телефона полностью
            </div>
          </div>
          <div class="form-group">
            <label
              for="sex"
              class="form-label"
              >Пол</label
            >
            <select
              class="form-select"
              v-bind="$v.clientRegForm.sex"
              name="sex"
              id="sex"
            >
              <option
                value=""
                selected
                disabled
              >
                Выберите пол
              </option>
              <option value="male">Мужчина</option>
              <option value="female">Женщина</option>
            </select>
          </div>
          <div class="form-group">
            <label
              for="client-groups"
              class="form-header"
              >Группа клиентов <span class="required">*</span></label
            >
            <select
              class="client-groups"
              id="client-groups"
              v-model="$v.clientRegForm.clientGroup.$model"
              :class="{
                'form-input_error': $v.clientRegForm.clientGroup.$error,
              }"
              @blur="$v.clientRegForm.clientGroup.$touch()"
              multiple
              name="client-groups"
            >
              <option
                class="client-groups__option"
                value="vip"
              >
                VIP
              </option>
              <option
                class="client-groups__option"
                value="problematic"
              >
                Проблемные
              </option>
              <option
                class="client-groups__option"
                value="oms"
              >
                ОМС
              </option>
            </select>
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.clientGroup.$dirty &&
                !$v.clientRegForm.clientGroup.required
              "
            >
              Поле обязательно для заполнения
            </div>
          </div>
          <div class="form-group">
            <label
              for="doctor"
              class="form-label"
              >Лечащий врач:</label
            >
            <select
              id="doctor"
              v-bind="$v.clientRegForm.selectedDoctor"
              name="doctor"
              class="form-select"
            >
              <option
                value=""
                selected
                disabled
              >
                Выберите врача
              </option>
              <option value="Иванов">Иванов</option>
              <option value="Захаров">Захаров</option>
              <option value="Чернышева">Чернышева</option>
            </select>
          </div>
          <div class="form-group">
            <div class="newsletter">
              <input
                type="checkbox"
                @click="getValue"
                name="subscribe"
                id="newsletter"
                class="newsletter-checkbox"
              />
              <label
                for="newsletter"
                class="newsletter-label"
                >Не отправлять смс</label
              >
            </div>
          </div>
        </div>
        <div class="address">
          <h2 class="heading">Адрес</h2>
          <div class="form-group">
            <label
              for="postcode"
              class="form-label"
              >Индекс</label
            >
            <input
              type="text"
              autocomplete="off"
              v-bind="$v.clientRegForm.postcode"
              class="form-input"
              id="postcode"
              placeholder="Введите индекс"
            />
          </div>
          <div class="form-group">
            <label
              for="country"
              autocomplete="off"
              class="form-label"
              >Страна</label
            >
            <input
              type="text"
              autocomplete="off"
              v-bind="$v.clientRegForm.country"
              class="form-input"
              id="country"
              placeholder="Введите страну"
            />
          </div>
          <div class="form-group">
            <label
              for="region"
              class="form-label"
              >Область</label
            >
            <input
              type="text"
              autocomplete="off"
              v-bind="$v.clientRegForm.region"
              class="form-input"
              id="region"
              placeholder="Введите область"
            />
          </div>
          <div class="form-group">
            <label
              for="city"
              class="form-label"
              >Город <span class="required">*</span></label
            >
            <input
              type="text"
              autocomplete="off"
              class="form-input"
              id="city"
              placeholder="Введите город"
              v-model="$v.clientRegForm.city.$model"
              :class="{ 'form-input_error': $v.clientRegForm.city.$error }"
              @blur="$v.clientRegForm.city.$touch()"
            />
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.city.$dirty && !$v.clientRegForm.city.required
              "
            >
              Поле обязательно для заполнения
            </div>
          </div>
          <div class="form-group">
            <label
              for="street"
              class="form-label"
              >Улица</label
            >
            <input
              type="text"
              v-bind="$v.clientRegForm.street"
              class="form-input"
              id="street"
              placeholder="Введите улицу"
            />
          </div>
          <div class="form-group">
            <label
              for="house"
              class="form-label"
              >Дом</label
            >
            <input
              type="text"
              autocomplete="off"
              v-bind="$v.clientRegForm.house"
              class="form-input"
              id="house"
              placeholder="Введите номер дома"
            />
          </div>
        </div>
        <div class="pasport">
          <h2 class="heading">Паспорт</h2>
          <div class="form-group">
            <label
              for="documentType"
              class="form-label"
              >Тип документа <span class="required">*</span></label
            >
            <select
              id="documentType"
              name="documentType"
              class="form-select"
              v-model="$v.clientRegForm.documentType.$model"
              :class="{
                'form-input_error': $v.clientRegForm.documentType.$error,
              }"
              @blur="$v.clientRegForm.documentType.$touch()"
            >
              <option
                value=""
                selected
                disabled
              >
                Выберите тип документа
              </option>
              <option value="pasport">Паспорт</option>
              <option value="birthCertificate">Свидетельство о рождении</option>
              <option value="driversLicense">Вод. удостоверение</option>
            </select>
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.documentType.$dirty &&
                !$v.clientRegForm.documentType.required
              "
            >
              Поле обязательно для заполнения
            </div>
          </div>
          <div class="form-group">
            <label
              for="series"
              autocomplete="off"
              class="form-label"
              >Серия</label
            >
            <input
              type="text"
              autocomplete="off"
              v-bind="$v.clientRegForm.series"
              class="form-input"
              id="series"
              placeholder="Введите серию"
            />
          </div>
          <div class="form-group">
            <label
              for="number"
              autocomplete="off"
              class="form-label"
              >Номер</label
            >
            <input
              type="text"
              autocomplete="off"
              v-model="clientRegForm.number"
              class="form-input"
              id="number"
              @input="onlyNumbers"
              placeholder="Введите номер"
            />
          </div>
          <div class="form-group">
            <label
              for="issuedBy"
              autocomplete="off"
              class="form-label"
              >Кем выдан</label
            >
            <input
              type="text"
              autocomplete="off"
              v-bind="$v.clientRegForm.issuedBy"
              class="form-input"
              id="issuedBy"
              placeholder="Введите кем выдан"
            />
          </div>
          <div class="form-group">
            <label
              for="issuedDate"
              autocomplete="off"
              class="form-label"
              >Дата выдачи <span class="required">*</span></label
            >
            <input
              type="text"
              autocomplete="off"
              class="form-input"
              id="issuedDate"
              placeholder="Введите дату (ДД/ММ/ГГГГ)"
              v-model="$v.clientRegForm.issueDate.$model"
              :class="{ 'form-input_error': $v.clientRegForm.issueDate.$error }"
              @blur="$v.clientRegForm.issueDate.$touch()"
              @input="onDateInput"
            />
            <div
              class="form_error"
              v-if="
                $v.clientRegForm.issueDate.$dirty &&
                !$v.clientRegForm.issueDate.required
              "
            >
              Поле обязательно для заполнения
            </div>
          </div>
        </div>
        <button
          class="create-btn"
          type="submit"
        >
          Создать
        </button>
      </form>
    </div>
  </div>
</template>

<script>
  import { required, minLength, alpha } from "vuelidate/lib/validators";
  export default {
    data() {
      return {
        clientRegForm: {
          firstName: "",
          middleName: "",
          lastName: "",
          day: "",
          month: "",
          year: "",
          phoneNumber: "",
          sex: "",
          clientGroup: [],
          selectedDoctor: "",
          newsletter: false,
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
          issueDate: "",
        },
      };
    },
    methods: {
      getValue() {
        this.clientRegForm.newsletter === false
          ? (this.clientRegForm.newsletter = true)
          : (this.clientRegForm.newsletter = false);
      },
      onSubmit() {
        this.$v.$touch();
        if (this.$v.$invalid) {
          return;
        }
        alert("Новый клиент успешно создан");
      },
      onDateInput(event) {
        const cleanedInput = event.target.value.replace(/\D/g, "");
        if (cleanedInput.length <= 2) {
          this.clientRegForm.issueDate = cleanedInput;
        } else if (cleanedInput.length <= 4) {
          this.clientRegForm.issueDate =
            cleanedInput.slice(0, 2) + "/" + cleanedInput.slice(2);
        } else {
          this.clientRegForm.issueDate =
            cleanedInput.slice(0, 2) +
            "/" +
            cleanedInput.slice(2, 4) +
            "/" +
            cleanedInput.slice(4, 8);
        }
      },
      telMask(event) {
        let unmaskedValue = event.target.value.replace(/\D/g, "");
        let formattedValue = "";

        if (unmaskedValue.length > 0) {
          formattedValue += "(" + unmaskedValue.substring(0, 3);

          if (unmaskedValue.length >= 4) {
            formattedValue += ") " + unmaskedValue.substring(3, 6);
          }
          if (unmaskedValue.length >= 7) {
            formattedValue += "-" + unmaskedValue.substring(6, 10);
          }
        }

        this.clientRegForm.phoneNumber = formattedValue;
      },
      onlyNumbers(event) {
        let unmaskedValue = event.target.value.replace(/\D/g, "");
        this.clientRegForm[event.target.id] = unmaskedValue;
      },
    },
    validations: {
      clientRegForm: {
        lastName: {
          required,
          minLength: minLength(3),
          alpha,
        },
        firstName: {
          required,
          minLength: minLength(3),
          alpha,
        },
        middleName: {
          minLength: minLength(3),
          alpha,
        },
        day: {
          required,
        },
        month: {
          required,
        },
        year: {
          required,
          minLength: minLength(4),
        },
        phoneNumber: {
          required,
          minLength: minLength(12),
        },
        clientGroup: {
          required,
        },
        city: {
          required,
        },
        documentType: {
          required,
        },
        issueDate: {
          required,
        },
      },
    },
  };
</script>

<style lang="scss">
  @import "./styles/main.sass";
</style>
