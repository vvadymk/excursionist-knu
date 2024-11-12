<template>
  <div>
    <section
      id="pricing"
      aria-label="Pricing"
      class="px-4 py-12 mx-auto sm:py-24 max-w-7xl sm:px-6 lg:px-8"
    >
      <div class="px-4 mx-auto max-w-7xl sm:px-6 lg:px-8">
        <div class="md:text-center">
          <h2 class="text-3xl tracking-tight text-slate-900 font-display sm:text-4xl md:text-5xl">
            Der unbezahlbare Wert eines Lächelns
          </h2>
          <p class="mt-4 text-lg text-slate-400">
            Verleihe deinen Geschichten eine Bühne, die so einzigartig ist wie deine Bilder
          </p>
          <p class="flex justify-center pt-8 text-lg text-slate-400">
            <UPricingToggle 
              v-model="isYearly" 
              class="max-w-xs" 
              left="Monatlich" 
              right="Jährlich"
            />
          </p>
        </div>
        <div class="grid max-w-2xl grid-cols-1 mt-12 -mx-4 gap-y-10 sm:mx-auto lg:-mx-8 lg:max-w-none lg:grid-cols-4 xl:mx-0 xl:gap-x-8">
          <UPricingCard
          v-for="price in prices" :key="price.title"
            :title="price.title"
            :price="isYearly ? price.price.yearly : price.price.monthly"
            :discount="isYearly ? price.discount.yearly : price.discount.monthly"
            cycle="/monatlich"
            :highlight="false"
            orientation="vertical"
            align="bottom"
            :features="price.features"
            class="shadow-xl"
            :ui="{
              amount: {
                cycle: 'text-clip'
              },
              features: {
                item: {
                  label: 'text-clip'
                }
              }
            }"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const isYearly = ref(false)

const prices = [
  {
    title: "Starter",
    price: { 
      monthly: "7€",
      yearly: "5€"
    },
    discount: { 
      monthly: "5€",
      yearly: "3€"
    },
    features: [
      '10 GB',
      'Unbegrenzte Galerien', 
      'Personalisierbare Galerien', 
      'Zugriff auf Templates', 
      'Wasserzeichen (Eigen oder Vorlage)',
      'Inkl. Fotografenprofil mit Social Media '
    ]
  },
  {
    title: "Basic",
    price: { 
      monthly: "10€",
      yearly: "8€"
    },
    discount: { 
      monthly: "6€",
      yearly: "5€"
    },
    features: [
      '30 GB',
      'Unbegrenzte Galerien', 
      'Personalisierbare Galerien', 
      'Zugriff auf Templates', 
      'Wasserzeichen (Eigen oder Vorlage)',
      'Inkl. Fotografenprofil mit Social Media '
    ]
  },
  {
    title: "Plus",
    price: { 
      monthly: "19€",
      yearly: "14€"
    },
    discount: { 
      monthly: "14€",
      yearly: "10€"
    },
    features: [
      '75 GB',
      'Unbegrenzte Galerien', 
      'Personalisierbare Galerien', 
      'Zugriff auf Templates', 
      'Wasserzeichen (Eigen oder Vorlage)',
      'Inkl. Fotografenprofil mit Social Media '
    ]
  },
  {
    title: "Pro",
    price: { 
      monthly: "42€",
      yearly: "32€"
    },
    discount: { 
      monthly: "35€",
      yearly: "27€"
    },
    features: [
      '750 GB',
      'Unbegrenzte Galerien', 
      'Personalisierbare Galerien', 
      'Zugriff auf Templates', 
      'Wasserzeichen (Eigen oder Vorlage)',
      'Inkl. Fotografenprofil mit Social Media '
    ]
  },
]
</script>
