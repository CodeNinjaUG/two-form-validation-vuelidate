<template>
  <form @submit.prevent="submitForm2" class="mt-8 grid grid-cols-6 gap-6">
    <div class="col-span-6 sm:col-span-3">
      <label for="FirstName" class="block text-sm font-medium text-gray-700">
        First Name
      </label>
      <span
        v-for="err in v$.firstname.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="text"
        v-model="v$.firstname.$model"
        class="mt-1 w-full rounded-md bg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6 sm:col-span-3">
      <label for="LastName" class="block text-sm font-medium text-gray-700">
        Last Name
      </label>
      <span
        v-for="err in v$.lastname.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="text"
        v-model="v$.lastname.$model"
        class="mt-1 w-full rounded-md bg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6">
      <label for="Email" class="block text-sm font-medium text-gray-700">
        Email
      </label>
      <span
        v-for="err in v$.email.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="email"
        v-model="v$.email.$model"
        class="mt-1 w-full rounded-mdbg-white text-sm text-gray-700 shadow-sm h-10 px-2 border border-gray-800"
      />
    </div>

    <div class="col-span-6 sm:col-span-3">
      <label for="Password" class="block text-sm font-medium text-gray-700">
        Password
      </label>
      <span
        v-for="err in v$.password.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="password"
        v-model="v$.password.$model"
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
        v-for="err in v$.confirm_password.$errors"
        :key="err.$uid"
        class="text-red-500"
      >
        {{ err.$message }}
      </span>
      <input
        type="password"
        v-model="v$.confirm_password.$model"
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
import { useVuelidate } from "@vuelidate/core";
import { required, email, sameAs } from "@vuelidate/validators";
export default {
  setup() {
    const individual = reactive({
      firstname: "",
      lastname: "",
      email: "",
      password: "",
      confirm_password: "",
    });

    const rules = computed(() => ({
      firstname: { required },
      lastname: { required },
      email: { required, email },
      password: { required },
      confirm_password: { required, sameAs: sameAs(individual.password) },
    }));
    const v$ = useVuelidate(rules, individual);
    const submitForm2 = async () => {
      const result = await v$.value.$validate();
      if (result) {
        console.log(result);
        console.log({ ...individual });
      }
    };
    return {
      v$,
      individual,
      submitForm2,
    };
  },
};
</script>
