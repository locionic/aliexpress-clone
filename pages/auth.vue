<template>
  <div id="AuthPage" class="w-full bg-white h-[100vh]">
    <div class="w-full items-center justify-center p-5 border-b border-b-gray-300">
      <NuxtLink to="/" class="min-w-[170px]">
        <img src="/AliExpress-logo.png" alt="AliExpress logo" width="170">
      </NuxtLink>
    </div>
    <div class="max-w-[400px] mx-auto px-2">
      <div class="text-center my-6">
        Login / Register
      </div>
      <button class="flex items-center justify-center gap-3 p-1.5 w-full border hover:bg-gray-100 rounded-full text-lg font-semibold" @click="login('google')">
        <img src="/google-logo.png" alt="Google logo" class="w-full max-w-[30px]">
        <div>Google</div>
      </button>
      <button class="mt-4 flex items-center justify-center gap-3 p-1.5 w-full border hover:bg-gray-100 rounded-full text-lg font-semibold" @click="login('github')">
        <img src="/github-logo.png" alt="Github logo" class="w-full max-w-[30px]">
        <div>Github</div>
      </button>
    </div>
  </div>
</template>
<script setup>
const client = useSupabaseClient()
const user = useSupabaseUser()

watchEffect(() => {
  if (user.value) {
    return navigateTo('/')
  }
})

const login = async (prov) => {
  const { data, error } = await client.auth.signInWithOAuth({
    provider: prov
  })
}

</script>