<template>
  <form @submit.prevent="submitForm" class="mt-8 grid grid-cols-6 gap-6">
    <div class="col-span-6 sm:col-span-3">
      <label for="FirstName" class="block text-sm font-medium text-gray-700">
        Company Name
      </label>
      <span
        v-for="err in v$.companyname.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="text"
        v-model="v$.companyname.$model"
        class="mt-1 w-full rounded-md bg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6 sm:col-span-3">
      <label for="LastName" class="block text-sm font-medium text-gray-700">
        Registration Number
      </label>
      <span
        v-for="err in v$.registration_no.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="text"
        v-model="v$.registration_no.$model"
        class="mt-1 w-full rounded-md bg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6">
      <label for="ComapnyEmail" class="block text-sm font-medium text-gray-700">
        Company Email
      </label>
      <span
        v-for="err in v$.companymail.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="email"
        v-model="v$.companymail.$model"
        class="mt-1 w-full rounded-md bg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6 sm:col-span-3">
      <label for="Password" class="block text-sm font-medium text-gray-700">
        Company Password
      </label>
      <span
        v-for="err in v$.companypassword.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="password"
        v-model="v$.companypassword.$model"
        class="mt-1 w-full rounded-md bg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6 sm:col-span-3">
      <label
        for="PasswordConfirmation"
        class="block text-sm font-medium text-gray-700"
      >
        Password Confirmation
      </label>
      <span
        v-for="err in v$.company_confirm_password.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="password"
        v-model="v$.company_confirm_password.$model"
        class="mt-1 w-full rounded-md bg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6 sm:flex sm:items-center sm:gap-4">
      <button
        class="inline-block shrink-0 rounded-md border border-blue-600 bg-blue-600 px-12 py-3 text-sm font-medium text-white transition hover:bg-transparent hover:text-blue-600 focus:outline-none focus:ring active:text-blue-500"
      >
        Create an account
      </button>

      <p class="mt-4 text-sm text-gray-500 sm:mt-0">
        Already have an account?
        <a href="#" class="text-gray-700 underline">Log in</a>.
      </p>
    </div>
  </form>
</template>
<script>
import { reactive, computed } from "vue";
import { required, email, sameAs, minLength } from "@vuelidate/validators";
import useVuelidate from "@vuelidate/core";
export default {
  setup() {
    const company = reactive({
      companyname: "",
      registration_no: "",
      companymail: "",
      companypassword: "",
      company_confirm_password: "",
    });

    const rules = computed(() => ({
      companyname: { required },
      registration_no: { required },
      companymail: { required, email },
      companypassword: { required },
      company_confirm_password: { required, sameAs: sameAs(company.password) },
    }));
    const v$ = useVuelidate(rules, company);
    const submitForm = async () => {
      const result = await v$.value.$validate();
      console.log(v$);
      console.log(result);
      if (result) {
        console.log(result);
        console.log({ ...company });
      }
    };
    return {
      company,
      submitForm,
      v$,
    };
  },
};
</script>
