<template>
  <section class="py-[200px] flex flex-col items-center justify-center px-4">
    <div class="text-[32px] font-semibold text-dark mb-4">Create Companies</div>
    <form class="w-full card" @submit.prevent="createCompany">
      <div class="form-group">
        <label for="" class="text-grey">Name</label>
        <input type="text" class="input-field" v-model="company.name" />
      </div>

      <button type="submit" class="w-full btn btn-primary mt-[14px]">
        Continue
      </button>

      
    </form>
  </section>
</template>
<script>
export default {
  middleware: "auth",
  data() {
    return {
      company: {
        name: "",
      },
    };
  },
  methods: {
    async createCompany() {
      try {
        //    Send Registration Data to the API
        const create = await this.$axios.post("/company", this.company);
          this.$router.push({
            name: "companies-id",
            params: { id: create.data.result.id },
          });
        console.log(`COBAK`,create);
      } catch (error) {
        
      }
    },
  },
};
</script>
