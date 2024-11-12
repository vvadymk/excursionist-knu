<template>
   <footer class="bg-white border-t-[1px] border-gray-200">
    <div class="px-6 py-8 mx-auto max-w-7xl md:flex md:items-center md:justify-between lg:px-8">
      <div class="flex flex-col items-center justify-center gap-4 md:space-x-6 md:gap-0 md:flex-row md:order-2">
        <UForm @submit="createProfile"  :state="state" class="flex flex-row items-center h-10 max-w-lg gap-2 mx-auto">
          <UFormGroup name="email" class="flex-1 border-none rounded-full font-roboto">
            <UInput placeholder="E-Mail hier eintragen" v-model="state.email" size="lg" />
          </UFormGroup>

          <UButton 
            type="submit" 
            size="lg"
            class="block w-1/2 text-center md:px-4" 
            color="primary"
            :ui="{ rounded: 'rounded' }"
          >
            Zur Warteliste
          </UButton>
        </UForm>
        <a v-for="item in navigation" :key="item.name" :href="item.href" target="_blank" class="text-gray-400 hover:text-gray-500">
          <span class="sr-only">{{ item.name }}</span>
          <component :is="item.icon" class="w-6 h-6" aria-hidden="true" />
        </a>
      </div>
      <div class="flex mt-4 space-x-6 md:mt-8 md:order-1 md:mt-0">
        <p class="flex self-center text-xs leading-5 text-center text-gray-500">&copy; 2024 Excursionist. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const toast = useToast()

const state = reactive({
  email: null,
})

async function createProfile() {
  const supabase = useSupabaseClient();
  try {
    const { data, error } = await supabase.auth.signUp({
      email: state.email,
      password: 'example-password',
    })

    if (error) {
      throw new Error(error);
    }

    toast.add({ title: 'Email successfully sent' });
    
    return data
  } catch(e) {
    console.error('Error: ', e);
    toast.add({ title: 'Error creating profile', description: e.message });
  }
}
</script>
