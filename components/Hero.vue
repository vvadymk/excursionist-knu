<template>
  <div class="relative flex flex-col justify-center h-screen px-4 mx-auto text-center -top-24 max-w-7xl sm:px-6 lg:px-8">
      <h1 class="max-w-5xl mx-auto text-3xl font-medium tracking-tight font-display text-slate-900 sm:text-7xl">
        <span class="text-blue-600 whitespace-nowrap">
        Coming soon:
        </span>
        Erwecke deine Bilder zum Leben mit 
        <span class="relative">
          <svg
            aria-hidden="true"
            viewBox="0 0 418 42"
            class="absolute left-0 top-2/3 h-[0.58em] w-full fill-blue-300/70"
            preserveAspectRatio="none"
          >
          <path d="M203.371.916c-26.013-2.078-76.686 1.963-124.73 9.946L67.3 12.749C35.421 18.062 18.2 21.766 6.004 25.934 1.244 27.561.828 27.778.874 28.61c.07 1.214.828 1.121 9.595-1.176 9.072-2.377 17.15-3.92 39.246-7.496C123.565 7.986 157.869 4.492 195.942 5.046c7.461.108 19.25 1.696 19.17 2.582-.107 1.183-7.874 4.31-25.75 10.366-21.992 7.45-35.43 12.534-36.701 13.884-2.173 2.308-.202 4.407 4.442 4.734 2.654.187 3.263.157 15.593-.78 35.401-2.686 57.944-3.488 88.365-3.143 46.327.526 75.721 2.23 130.788 7.584 19.787 1.924 20.814 1.98 24.557 1.332l.066-.011c1.201-.203 1.53-1.825.399-2.335-2.911-1.31-4.893-1.604-22.048-3.261-57.509-5.556-87.871-7.36-132.059-7.842-23.239-.254-33.617-.116-50.627.674-11.629.54-42.371 2.494-46.696 2.967-2.359.259 8.133-3.625 26.504-9.81 23.239-7.825 27.934-10.149 28.304-14.005.417-4.348-3.529-6-16.878-7.066Z" />
          </svg>
          <span class="relative text-blue-600 whitespace-nowrap">
            Excursionist
          </span>
        </span>
      </h1>
      <p class="max-w-2xl pt-4 mx-auto text-xl tracking-tight text-slate-700">
        Die Online-Galerie für Fotografen – intuitiv, modern, zuverlässig!
      </p>
        <UForm @submit="createProfile"  :state="state" class="flex flex-col gap-2 pt-12 mx-auto md:flex-row">
          <UFormGroup name="email" class="flex-1 border-none rounded-full min-w-[300px] font-robot md:min-w-[500px]">
            <UInput type="email" variant="outline" placeholder="E-Mail hier eintragen" v-model="state.email" size="xl" />
          </UFormGroup>

          <UButton 
            type="submit" 
            size="xl"
            class="flex justify-center w-full md:w-fit md:px-2"
            color="primary"
            :disabled="!state.email"
            :ui="{ rounded: 'rounded' }"
          >
            Zur Warteliste hinzufügen
          </UButton>
        </UForm>
      <div class="absolute left-0 right-0 pt-8 bottom-10">
        <UButton 
            icon="i-heroicons-chevron-double-down"
            size="xl"
            type="submit" 
            class="px-8 py-1"
            to="#CTA" 
            :ui="{ rounded: 'rounded-full' }"
          />

      </div>
  </div>
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
