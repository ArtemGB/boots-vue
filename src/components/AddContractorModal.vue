<template>
  <b-modal
    id="add-modal"
    centered
    title="Добавление"
    @ok="AddContractor"
    hide-footer
  >
    <validation-observer ref="observer" v-slot="{ handleSubmit }">
      <b-form @submit.stop.prevent="handleSubmit(onSubmit(bvModal))">
        <validation-provider
          name="Название"
          :rules="{ required: true, min: 3 }"
          v-slot="validationContext"
        >
          <b-input-group class="mb-2" prepend="Название">
            <b-form-input
              v-model="Contractor.Name"
              placeholder="Введите название"
              :state="getValidationState(validationContext)"
            ></b-form-input>
          </b-input-group>
          <b-form-invalid-feedback id="input-1-live-feedback">{{
            validationContext.errors[0]
          }}</b-form-invalid-feedback>
        </validation-provider>

        <validation-provider
          name="ContractorType"
          :rules="{ required: true }"
          v-slot="validationContext"
        >
          <b-input-group
            class="mb-2"
            prepend="Тип"
            invalid-feedback="Заполните поле"
          >
            <b-form-select
              class="mb-2"
              v-model="Contractor.Type"
              :options="TypeOptions"
              :state="getValidationState(validationContext)"
            ></b-form-select>
            <b-form-invalid-feedback id="input-2-live-feedback">{{
              validationContext.errors[0]
            }}</b-form-invalid-feedback>
          </b-input-group>
        </validation-provider>

        <validation-provider
          name="ИНН"
          :rules="{ reauired: true }"
          v-slot="validationContext"
        >
          <b-input-group
            class="mb-2"
            prepend="ИНН"
            invalid-feedback="Заполните поле"
          >
            <b-form-input
              v-model="Contractor.INN"
              placeholder="Введите инн"
              :state="getValidationState(validationContext)"
            ></b-form-input>
            <b-form-invalid-feedback>{{
              validationContext.errors[0]
            }}</b-form-invalid-feedback>
          </b-input-group>
        </validation-provider>
        <validation-provider
          name="КПП"
          :rules="{ required: true }"
          v-slot="validationContext"
        >
          <b-input-group
            class="mb-2"
            prepend="КПП"
            v-if="Contractor.Type == 'Legal'"
            invalid-feedback="Заполните поле"
          >
            <b-form-input
              v-model="Contractor.KPP"
              placeholder="Введите кпп"
              :state="getValidationState(validationContext)"
            ></b-form-input>
            <b-form-invalid-feedback id="input-2-live-feedback">{{
              validationContext.errors[0]
            }}</b-form-invalid-feedback>
          </b-input-group>
        </validation-provider>
        <b-button id="submit-btn" type="submit" variant="primary">Добавить</b-button>
      </b-form>
    </validation-observer>
  </b-modal>
</template>

<script>
export default {
  name: "AddContractorModal",
  data: function () {
    return {
      Contractor: {
        Name: "",
        INN: "",
        KPP: "",
        Type: null,
      },
      TypeOptions: [
        { value: null, text: "Выберите тип котрагента" },
        { value: "Legal", text: "Юр. Лицо" },
        { value: "Individual", text: "ИП" },
      ],
    };
  },
  methods: {
    AddContractor: async function () {
      await fetch("http://localhost:5000/Home/Create", {
        method: "POST",
        headers: {
          "Content-Type": "application/json-patch+json",
        },
        body: JSON.stringify(this.Contractor),
      }).then((response) => response.json());
    },
    getValidationState({ dirty, validated, valid = null }) {
      return dirty || validated ? valid : null;
    },
    onSubmit(){
      this.$refs['add-modal'].hide();
    }
  },
};
</script>

<style>
</style>