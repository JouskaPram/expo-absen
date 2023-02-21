<template>
  <div>
    <form method="post" @submit.prevent="Signup()">
      <input
        type="email"
        v-model="email"
        class="bg-slate-300 border border-slate-600"
      />
      <input
        type="password"
        v-model="password"
        class="bg-slate-300 border border-slate-600"
      />
      <button
        type="submit"
        class="py-2 px-5 text-center font-semibold text-white bg-sky-500 hover:bgsky-400 rounded-full"
      >
        Regis
      </button>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const email = ref();
const password = ref();
async function Signup() {
  const { user, data, error } = await supabase.auth.signUp({
    email: email.value,
    password: password.value,
  });
  console.log(user);
}
</script>
