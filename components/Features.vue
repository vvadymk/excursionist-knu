<template>
  <div>
    <section
      id="features"
      aria-label="Features for running your books"
      class="relative pt-20 pb-12 overflow-hidden bg-slate-900 sm:py-32"
    >
      <div class="relative px-4 mx-auto max-w-7xl sm:px-6 lg:px-8">
        <div class="max-w-2xl md:mx-auto md:text-center xl:max-w-none">
          <h2 class="text-3xl tracking-tight text-white font-display sm:text-4xl md:text-5xl">
            Erwecke deine Bilder zum Leben
          </h2>
          <p class="w-full mx-0 mt-4 text-lg text-left md:w-1/2 md:mx-auto md:text-center text-slate-400">
            Entfalte deine Kreativität mit hoher Nutzerfreundlichkeit, Designflexibilität und 
            professioneller Präsentation
          </p>
        </div>
        <ClientOnly>
          <TabGroup
            as="div"
            class="grid items-center grid-cols-1 pt-10 mt-16 gap-y-2 sm:gap-y-6 md:mt-20 lg:grid-cols-12 lg:pt-0"
            vertical
            :defaultIndex="0"
            :selected-index="selectedTab"
            @change="changeTab"
          >
            <div class="flex pb-4 -mx-4 overflow-x-auto sm:mx-0 sm:overflow-visible sm:pb-0 lg:col-span-5">
              <TabList class="relative z-10 flex px-4 gap-x-4 whitespace-nowrap sm:mx-auto sm:px-0 lg:mx-0 lg:block lg:gap-x-0 lg:gap-y-1 lg:whitespace-normal">
                <div
                  class="relative px-4 py-1 rounded-full group lg:rounded-l-xl lg:rounded-r-none lg:p-6"
                  :class="selectedTab === index ? 'bg-white lg:bg-white/10 lg:ring-1 lg:ring-inset lg:ring-white/10' : 'hover:bg-white/10 lg:hover:bg-white/5'"
                  v-for="(feature, index) in features"
                  :key="feature.title"
                >
                  <h3>
                    <Tab
                      class="text-lg md:text-blue-100 font-display ui-not-focus-visible:outline-none md:hover:text-white lg:text-white"
                      :class="selectedTab === index ? 'text-slate-900' : 'text-blue-100'"
                    >
                      <span class="absolute inset-0 rounded-full lg:rounded-l-xl lg:rounded-r-none" />
                      {{ feature.title }}
                    </Tab>
                  </h3>

                  <p v-html="feature.description" class="hidden mt-2 text-sm text-blue-100 lg:block group-hover:text-white" />
                </div>
              </TabList>
            </div>
            <TabPanels class="lg:col-span-7">
              <TabPanel
                v-for="feature in features"
                :unmount="false"
              >
                <div class="relative sm:px-6 lg:hidden">
                  <div class="absolute -inset-x-4 bottom-[-4.25rem] top-[-6.5rem] bg-white/10 ring-1 ring-inset ring-white/10 sm:inset-x-0 sm:rounded-t-xl" />
                    <p v-html="feature.description" class="relative max-w-3xl pt-4 mx-auto text-base text-center text-white md:pt-0" />
                  </div>
                  <div class="mt-10 w-[300px] mx-auto md:w-[45rem] overflow-hidden rounded-xl bg-slate-50 shadow-xl shadow-blue-900/20 sm:w-auto lg:mt-0 lg:w-[67.8125rem]">
                  <NuxtImg
                    class="relative z-50 w-full"
                    :src="`/images/${feature.image}.png`"
                    alt=""
                    />
                </div>
              </TabPanel>
            </TabPanels>
          </TabGroup>
          </ClientOnly>
      </div>
    </section>
  </div>
</template>

<script setup>
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from '@headlessui/vue'

const features = [
  {
    title: 'Hohe Benutzerfreundlichkeit',
    description:
      "Intuitive Oberfläche für eine effiziente und <br> angenehme Nutzungserfahrung.",
    image: 'feature1',
  },
  {
    title: 'Individuelles Design',
    description:
      "Nutze unsere Vorlagen und passe das Design <br> nach deinem Geschmack an.",
    image: 'feature2',
  },
  {
    title: 'Marketing Boost',
    description:
      "Steigere deine Sichtbarkeit mit deinem <br> Fotografenprofil am Ende jeder Galerie.",
    image: 'feature3',
  },
  // {
  //   title: 'Wasserzeichen-Schutz',
  //   description:
  //     'Schütze deine Bilder mit individuellen Wasserzeichen <br> vor unerlaubter Nutzung.',
  //   image: 'vat-returns',
  // },
]

const selectedTab = ref(0)

function changeTab(index) {
  selectedTab.value = index
}
</script>
