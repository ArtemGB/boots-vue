<template>
    <div>
      <b-modal id="add-modal" centered title="Добавление">
      <b-input-group class="mb-2" prepend="Название">
        <b-form-input
          v-model="Name"
          placeholder="Введите название"
        ></b-form-input>
      </b-input-group>
      <b-input-group prepend="Тип">
        <b-form-select v-model="Type" :options="TypeOptions"></b-form-select>
      </b-input-group>
      <b-input-group prepend="ИНН">
        <b-form-input v-model="Name" placeholder="Введите инн"></b-form-input>
      </b-input-group>
      <b-input-group prepend="КПП" v-if="Type == 'Legal'">
        <b-form-input v-model="Name" placeholder="Введите кпп"></b-form-input>
      </b-input-group>
    </b-modal>
    </div>
</template>

<script>
export default {
  name: "AddContractorModal",
  data: function () {
    return {
      Name: String,
      Type: null,
      TypeOptions: [
        { value: null, text: "Выберите тип котрагента" },
        { value: "Legal", text: "Юр. Лицо" },
        { value: "Individual", text: "ИП" },
      ],
    };
  }
};
</script>

<style>
</style>