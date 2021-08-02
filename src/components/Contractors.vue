<template>
  <div>
    <b-table
      striped
      hover
      small
      :items="contractors"
      :fields="fields"
      :busy="isLoading"
    >
      <template #table-busy>
        <div class="text-center text-danger my-2">
          <b-spinner class="align-middle"></b-spinner>
          <strong>Загрузка...</strong>
        </div>
      </template>
      <template #cell(AddDeleteButtons)="data">
        <div>
          <b-button-group>
            <b-button variant="info">Редактировать</b-button>
            <b-button
              variant="danger"
              v-on:click="DeleteContractor(data.item.Id)"
              >Удалить</b-button
            >
          </b-button-group>
        </div>
      </template>
    </b-table>
     <b-button @click="$bvModal.show('add-modal')">Добавить котрагента</b-button>
    <AddContractorModal/>
  </div>
</template>

<script>
import AddContractorModal from "./AddContractorModal.vue";

export default {
  name: "Contractors",
  data: function () {
    return {
      fields: [
        {
          key: "Id",
          label: "№",
        },
        {
          key: "Name",
          label: "Название",
        },
        {
          key: "FullName",
          label: "Полное название",
        },
        {
          key: "Type",
          label: "Тип",
        },
        {
          key: "Inn",
          label: "ИНН",
        },
        {
          key: "Kpp",
          label: "КПП",
        },
        {
          key: "AddDeleteButtons",
          label: "",
        },
      ],
      contractors: [],
      isLoading: true,
      showAddModal: false,
    };
  },
  created: function () {
    this.GetContractors();
  },
  updated: function () {
    this.GetContractors();
  },
  components: {
    AddContractorModal,
  },
  methods: {
    Add: function(){
      this.showAddModal = !this.showAddModal;
      console.log(this.showAddModal);
    },
    GetContractors: async function () {
      await fetch("http://localhost:5000/Home/Index")
        .then((response) => response.json())
        .then((data) => {
          this.contractors = data;
          this.isLoading = false;
        });
    },
    DeleteContractor: function (contrId) {
      if (
        window.confirm("Вы действительно хотите удалить даннго котрагента?")
      ) {
        fetch("http://localhost:5000/Home/delete/" + contrId, {
          method: "DELETE",
        });
      }
    },
  },
};
</script>