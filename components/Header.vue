<template>
  <UHeader>
    <template #logo>
      <h2 class="text-primary text-4xl font-bold">Excursionist</h2>
    </template>

    <template #right>
      <UHeaderLinks 
        class="w-[300px] justify-end"
        :links="links"
        :ui="{
          wrapper: 'gap-x-4 md:gap-x-8',
          active: 'text-slate-900',
          base: 'hover:text-blue-500 font-medium md:font-semibold'
        }"
      />
      <UButton 
            size="xl"
            type="button" 
            class="hidden px-6 py-1 ml-3 sm:block"
            to="#CTA" 
            :ui="{ rounded: 'rounded-full' }"
      >
        Zur Warteliste
      </UButton>
    </template>
  </UHeader>
</template>

<script setup>

const links = [{
  label: 'Preise',
  to: '/#preise'
}, {
  label: 'Funktionen',
  to: '/#funktionen'
}, {
  label: 'Über uns',
  to: '/#uberUns'
}]
</script>
