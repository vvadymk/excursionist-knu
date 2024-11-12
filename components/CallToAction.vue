<template>
<div 
  class="relative overflow-hidden text-white isolate bg-slate-900"
  :class="isFull ? 'py-12 sm:py-24' : 'pt-20 pb-8'"
>
  <div 
    :class="isFull ? 'grid grid-cols-1 mx-auto max-w-7xl lg:grid-cols-2' : 'flex justify-center'"
  >
    <NuxtImg
      v-if="!isFull"
      class="absolute -translate-x-1/2 -translate-y-1/2 left-1/2 top-1/2 max-w-none"
      src="/images/background-call-to-action.jpg"
      width="2347"
      height="1244"
      alt=""
    />
    <div class="z-10 order-2 px-6 pb-24 sm:pb-32 lg:px-8 md:order-none">
      <div 
        class="max-w-xl mx-auto lg:mr-0 lg:max-w-3xl"
        :class="isFull ? 'text-left' : 'text-center'"
      >
        <h2 class="pb-8 text-3xl font-bold tracking-tight md:pb-16 md:text-4xl">
          Melde dich an und sichere dir deinen exklusiven Einführungspreis zum Launch!
        </h2>
        <UForm @submit="createProfile"  :state="state" class="flex flex-col h-10 max-w-lg gap-2 mx-auto">
          <UFormGroup name="email" class="flex-1 pb-4 border-none rounded-full font-roboto">
            <UInput type="email" placeholder="E-Mail hier eintragen" v-model="state.email" size="xl" />
          </UFormGroup>

          <UButton 
            type="submit" 
            size="xl"
            class="block w-full text-center md:px-10" 
            color="white"
            :disabled="!state.email"
            :ui="{ rounded: 'rounded' }"
          >
            Zur Warteliste hinzufügen
          </UButton>
        </UForm>
      </div>
    </div>

    <div v-if="isFull" class="relative px-6 pb-8 md:pb-20 lg:static lg:px-8 ">
      <div class="max-w-xl mx-auto lg:mx-0 lg:max-w-lg">
        <h2 class="text-3xl font-bold tracking-tight text-white md:text-4xl">Warum zu SnapSphere wechseln?</h2>
        <ul class="mt-6 text-lg leading-8 text-white list-disc md:text-xl">
          <li class="ml-4"><strong>Uneingeschränkte Funktionen:</strong><br> Vollständiger Zugriff auf 
            alle Funktionen in allen Abonnenemts – Unterschiede nur beim Speicherplatz</li>
          <li class="ml-4"><strong>Benutzerfreundlich:</strong> <br>Intuitive Oberfläche für ansprechende Galerien</li>
          <li class="ml-4"><strong>Vielseitig:</strong><br> Ideal für Profis und Hobbyfotografen</li>
        </ul>
        <dl class="mt-10 space-y-4 text-lg leading-7 text-white md:text-xl">
          <p>
            <strong>Exklusives Einführungsangebot:</strong><br> Registriere dich jetzt mit deiner E-Mail-Adresse, 
            um spezielle Einführungspreise zu sichern und als Erster zu erfahren, wenn wir live gehen!
          </p>
        </dl>
      </div>
    </div>
  </div>
</div>
</template>

<script setup>
const props = defineProps({
  isFull: {
    type: Boolean,
    default: true
  }
})

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
