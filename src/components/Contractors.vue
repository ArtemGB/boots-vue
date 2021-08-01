<template>
  <div>
    <template v-if="isLoading">
      <b-spinner label="Loading..."></b-spinner>
    </template>
    <template v-else>
      <b-table striped hover :items="contractors"></b-table>
    </template>
  </div>
</template>

<script>
export default {
  name: "Contractors",
  data: function () {
    return {
      contractors: [],
      isLoading: true,
    };
  },
  created: function () {
    this.GetContractors();
  },
  methods: {
    GetContractors: async function () {
      await fetch('localhost:5000/Home/Index',{
        method: 'GET',
        headers:{
          accept: '*/*'
        }
      })
        .then((response) => response.json())
        .then(
          (data) => {
            this.contractors = data;
            this.isLoading = false;
          },
          (error) => alert(error.message)
        );
    },
  },
};
</script>