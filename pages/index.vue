<template>
  <section class="py-[200px] flex flex-col items-center justify-center px-4">
    <div class="text-[32px] font-semibold text-dark mb-4">Select Companies</div>
    <div class="w-full card">
      <div class="form-group">
        <label for="" class="text-grey">Companies</label>
        <p v-if="$fetchState.pending">Fetching Companies...</p>

        <select
          v-else
          name="companies"
          v-model="selectedCompany"
          class="appearance-none input-field form-icon-chevron_down"
        >
          <option
            :value="company.id"
            :key="company.id"
            v-for="company in companies"
          >
            {{ company.name }}
          </option>
        </select>
      </div>
        <button
        type="button"
        @click="openCompanies"
        class="w-full btn btn-primary mt-[14px]"
        :class="{ 'opacity-50 pointer-events-none': !selectedCompany }"
        :disabled="!selectedCompany"
      >
        Continue
      </button>
      <div class="text-center">Or</div>
        <NuxtLink :to="{ name: 'companies-create' }" class="w-full border btn btn-white">Create New Company</NuxtLink>   
      
    </div>
  </section>
</template>
<script>
export default {
  middleware: "auth",
  data() {
    return {
      companies: [],
      selectedCompany: "",
    };
  },
  async fetch() {
    const response = await this.$axios.$get("/company");
    this.companies = response.result.data;
  },
  methods: {
    openCompanies() {
      this.$router.push({
        name: "companies-id",
        params: { id: this.selectedCompany },
      });
    },
  },
};
</script>
