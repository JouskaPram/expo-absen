<template>
  <div>
    <form @submit.prevent="login()" method="post">
      <input
        type="email"
        class="bg-gray-300 border border-gray-600"
        v-model="email"
      />
      <input
        type="password"
        class="bg-gray-300 border border-gray-600"
        v-model="password"
      />
      <button
        type="submit"
        class="py-2 px-5 text-center font-semibold text-white bg-sky-500 rounded-md"
      >
        Masuk
      </button>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const email = ref();
const password = ref();
async function login() {
  const { data, error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  console.log(data);
}
</script>

<style lang="scss" scoped></style>
