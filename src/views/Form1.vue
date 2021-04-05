<template>
  <div>
    <form class="form" @submit.prevent="submitHandler">
      <div class="form__title">Create Client Form</div>
      <div>
        <label class="label label--req" for="surname">Surname</label>
        <input
            class="input"
            :class="{
              invalid:
                (this.$v.surname.$dirty && !this.$v.surname.required)
            }"
            type="text"
            name="surname"
            id="surname"
            v-model="surname"
        >
        <small
            class="input-invalid-message"
            v-if="this.$v.surname.$dirty && !this.$v.surname.required"
        >The field must not be empty!</small>
      </div>
      <div>
        <label class="label label--req" for="name">Name</label>
        <input
            class="input"
            :class="{
              invalid:
                (this.$v.name.$dirty && !this.$v.name.required)
            }"
            type="text"
            name="name"
            id="name"
            v-model="name"
        >
        <small
            class="input-invalid-message"
            v-if="this.$v.name.$dirty && !this.$v.name.required"
        >The field must not be empty!</small>
      </div>
      <div>
        <label class="label" for="patronymic">Patronymic</label>
        <input class="input" type="text" name="patronymic" id="patronymic">
      </div>
      <div>
        <label class="label label--req" for="bornDate">Born date</label>
        <input
            class="input"
            :class="{
              invalid:
                (this.$v.bornDate.$dirty && !this.$v.bornDate.required)
            }"
            type="date"
            id="bornDate"
            name="bornDate"
            value="2018-07-22"
            min="1900-01-01"
            max="2021-04-01"
            v-model="bornDate"
        >
      </div>
      <div>
        <label class="label label--req" for="phone">Phone</label>
        <div class="phone__field">
          <span class="phone__field-pre"><span>+7</span></span>
          <input
              class="input"
              :class="{
                invalid:
                  (this.$v.phone.$dirty && !this.$v.phone.required)
              }"
              type="tel"
              v-model="phone"
              name="phone"
              id="phone"
              placeholder="(555) 555-55-55"
              maxlength="15"
              v-phone
              pattern="[(][0-9]{3}[)] [0-9]{3}-[0-9]{2}-[0-9]{2}"
          />
        </div>
      </div>
      <div>
        <label class="label" for="gender">Gender</label>
        <div class="gender__body" id="gender">
          <div>
            <input class="input" type="radio" id="genderMale" value="Male" v-model="gender">
            <label for="genderMale">Male</label>
          </div>
          <div>
            <input class="input" type="radio" id="genderFemale" value="Female" v-model="gender">
            <label for="genderFemale">Female</label>
          </div>
        </div>
      </div>
      <div>
        <label class="label label--req" for="group">Client group</label>
        <multiselect
            id="group"
            :class="{
              invalid:
                (this.$v.group.$dirty && !this.$v.group.required)
            }"
            v-model="group"
            :options="multiOptions"
            :multiple="true"
            :close-on-select="false"
            :clear-on-select="false"
            :preserve-search="false"
            placeholder="Choose client group"
            label="val"
            track-by="val"
            :preselect-first="false">
          <template
              slot="selection"
              slot-scope="{ values, search, isOpen }"
          >
            <span class="multiselect__single" v-if="multiValue.length &amp;&amp; !isOpen">
              {{ multiValue.length }} categories selected
            </span>
          </template>
        </multiselect>
      </div>
      <div>
        <label class="label" for="therapist">Therapist</label>
        <multiselect
            id="therapist"
            v-model="selectValue"
            :options="selectOptions"
            :searchable="false"
            :close-on-select="false"
            :show-labels="false"
            label="val"
            placeholder="Choose therapist"
        ></multiselect>
      </div>
      <div class="checkbox">
        <input
            class="input"
            id="messageCheckbox"
            name="messageCheckbox"
            type="checkbox"
            checked="true"
        >
        <label class="label" for="messageCheckbox">Don't send SMS</label>
      </div>
      <div>
        <label class="label" for="index">Index</label>
        <input class="input" type="text" name="index" id="index">
      </div>
      <div>
        <label class="label" for="country">Country</label>
        <input class="input" type="text" name="country" id="country">
      </div>
      <div>
        <label class="label" for="region">Region</label>
        <input class="input" type="text" name="region" id="region">
      </div>
      <div>
        <label class="label label--req" for="city">City</label>
        <input
            class="input"
            :class="{
              invalid:
                (this.$v.city.$dirty && !this.$v.city.required)
            }"
            type="text"
            name="city"
            id="city"
            v-model="city"
        >
        <small
            class="input-invalid-message"
            v-if="this.$v.city.$dirty && !this.$v.city.required"
        >The field must not be empty!</small>
      </div>
      <div>
        <label class="label" for="street">Street</label>
        <input class="input" type="text" name="street" id="street">
      </div>
      <div>
        <label class="label" for="house">House</label>
        <input class="input" type="text" name="house" id="house">
      </div>
      <div>
        <label class="label label--req" for="document">Document type</label>
        <multiselect
            id="document"
            :class="{
              invalid:
                (this.$v.document.$dirty && !this.$v.document.required)
            }"
            v-model="document"
            :options="documentOptions"
            :searchable="false"
            :close-on-select="false"
            :show-labels="false"
            label="val"
            placeholder="Choose document type"
        ></multiselect>
      </div>
      <div>
        <label class="label" for="series">Series</label>
        <input class="input" type="text" name="series" id="series">
      </div>
      <div>
        <label class="label" for="number">Number</label>
        <input class="input" type="text" name="number" id="number">
      </div>
      <div>
        <label class="label" for="issuedBy">Issued by</label>
        <input class="input" type="text" name="issuedBy" id="issuedBy">
      </div>
      <div>
        <label class="label label--req" for="issuedWhen">Issued when</label>
        <input
            class="input"
            :class="{
              invalid:
                (this.$v.issuedWhen.$dirty && !this.$v.issuedWhen.required)
            }"
            type="date"
            id="issuedWhen"
            name="issuedWhen"
            value="2018-07-22"
            min="1900-01-01"
            max="2021-04-01"
            v-model="issuedWhen"
        >
      </div>
      <button type="submit" class="form__button">Create client</button>
      <p class="submit__message submit__ok" v-if="submitStatus === 'OK'">Thanks for your submission!</p>
      <p class="submit__message submit__err" v-if="submitStatus === 'ERROR'">Please fill the form correctly.</p>
    </form>
  </div>
</template>

<script>
import Vue from "vue"
import Multiselect from 'vue-multiselect'
import {required, minLength} from "vuelidate/lib/validators";

Vue.directive('phone', {
  bind(el) {
    el.oninput = function (e) {
      if (!e.isTrusted) {
        return;
      }

      const x = this.value.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,2})(\d{0,2})/);
      this.value = !x[2] ? x[1] : '(' + x[1] + ') ' + x[2] + '-' + x[3] + (x[4] ? '-' + x[4] : '');
      el.dispatchEvent(new Event('input'));
    }
  },
});

export default {
  data: () => ({
    multiValue: [],
    multiOptions: [
      {val: 'VIP'},
      {val: 'Problematic'},
      {val: 'OMS'},
    ],
    selectValue: [],
    selectOptions: [
      {val: 'Ivanov'},
      {val: 'Chernyshev'},
      {val: 'Zakharova'},
    ],
    documentValue: [],
    documentOptions: [
      {val: 'Passport'},
      {val: 'Birth certificate'},
      {val: 'Driver\'s license'},
    ],
    name: "",
    surname: "",
    bornDate: "",
    phone: "",
    group: "",
    gender: "",
    city: "",
    document: "",
    issuedWhen: "",
    submitStatus: ""
  }),
  validations: {
    name: {required},
    surname: {required},
    bornDate: {required},
    phone: {required},
    group: {required},
    city: {required},
    document: {required},
    issuedWhen: {required},
  },
  components: {
    Multiselect
  },
  methods: {
    submitHandler() {
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitStatus = 'ERROR'
      } else {
        setTimeout(() => {
          this.submitStatus = 'OK'
        }, 500)
      }
    },
  },
};

</script>