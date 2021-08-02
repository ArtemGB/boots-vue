<template>
  <div>
    <b-modal
      id="add-modal"
      centered
      title="Добавление"
      @ok="AddContractor"
      ref="modal"
    >
      <b-form ref="form">
        <b-input-group class="mb-2" prepend="Название">
          <b-form-input
            v-model="Contractor.Name"
            placeholder="Введите название"
            required
          ></b-form-input>
        </b-input-group>
        <b-input-group
          class="mb-2"
          prepend="Тип"
          invalid-feedback="Заполните поле"
        >
          <b-form-select
            class="mb-2"
            v-model="Contractor.Type"
            :options="TypeOptions"
            required
          ></b-form-select>
        </b-input-group>
        <b-input-group
          class="mb-2"
          prepend="ИНН"
          invalid-feedback="Заполните поле"
        >
          <b-form-input
            v-model="Contractor.INN"
            placeholder="Введите инн"
            required
          ></b-form-input>
        </b-input-group>
        <b-input-group
          class="mb-2"
          prepend="КПП"
          v-if="Contractor.Type == 'Legal'"
          invalid-feedback="Заполните поле"
        >
          <b-form-input
            v-model="Contractor.KPP"
            placeholder="Введите кпп"
            required
          ></b-form-input>
        </b-input-group>
      </b-form>
    </b-modal>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>