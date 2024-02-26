<template>
  <div id="app">
    <div class="container">
      <div class="client-reg-form">
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
            >Отчество (необязательно)</label
          >
          <input
            type="text"
            v-model.trim="$v.clientRegForm.middleName.$model"
            @blur="$v.clientRegForm.middleName.$touch()"
            class="form-input"
            :class="{ 'form-input_error': $v.clientRegForm.middleName.$error }"
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
              :class="{
                'form-input_error':
                  $v.clientRegForm.day.$error ||
                  $v.clientRegForm.month.$error ||
                  $v.clientRegForm.year.$error,
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
              @blur="isMonthSelect"
              :class="{
                'form-input_error':
                  $v.clientRegForm.day.$error ||
                  $v.clientRegForm.month.$error ||
                  $v.clientRegForm.year.$error,
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
              :class="{
                'form-input_error':
                  $v.clientRegForm.day.$error ||
                  $v.clientRegForm.month.$error ||
                  $v.clientRegForm.year.$error,
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
        <div class="form-group">
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
            maxlength="12"
            placeholder="+7__________"
            onfocus="if (this.value === '') { this.value = '+7'; }"
            v-model="$v.clientRegForm.phoneNumber.$model"
            @input="maskNumber"
            @blur="$v.clientRegForm.phoneNumber.$touch()"
            :class="{
              'form-input_error': $v.clientRegForm.phoneNumber.$error,
            }"
          />
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
            >Пол (необязательно)</label
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
            :class="{ 'form-input_error': $v.clientRegForm.clientGroup.$error }"
            @blur="$v.clientRegForm.clientGroup.$touch()"
            multiple
            required
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
            <label for="newsletter">Не отправлять смс</label>
            <input
              type="checkbox"
              class="newsletter-checkbox"
              @click="getValue"
              name="subscribe"
              id="newsletter"
            />
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
            v-bind="$v.clientRegForm.postcode"
            class="form-input"
            id="postcode"
            placeholder="Введите индекс"
          />
        </div>
        <div class="form-group">
          <label
            for="country"
            class="form-label"
            >Страна</label
          >
          <input
            type="text"
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
            v-bind="$v.clientRegForm.house"
            class="form-input"
            id="house"
            placeholder="Введите номер дома"
          />
        </div>
      </div>
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
          phoneNumber: "+7",
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
        },
      };
    },
    methods: {
      maskNumber() {
        const pattern = /^(\+7\d{0,11})$/;
        this.clientRegForm.phoneNumber = this.clientRegForm.phoneNumber.replace(
          /[^+\d]/g,
          ""
        );
        this.clientRegForm.phoneNumber = this.clientRegForm.phoneNumber.replace(
          pattern,
          "$1"
        );
        if (
          this.clientRegForm.phoneNumber.length === 1 &&
          this.clientRegForm.phoneNumber !== "+7"
        ) {
          this.clientRegForm.phoneNumber = "+7";
        }
      },
      isMonthSelect() {
        if (this.clientRegForm.month === "") {
          this.$v.clientRegForm.month.$touch();
        }
      },
      getValue() {
        this.clientRegForm.newsletter === false
          ? (this.clientRegForm.newsletter = true)
          : (this.clientRegForm.newsletter = false);
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
          minLength: minLength(2),
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
      },
    },
  };
</script>

<style lang="scss">
  @import "./styles/main.sass";
</style>
