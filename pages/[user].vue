<template>
    <div>

        <Head>
			<Title>{{ osoba.data[0].attributes.Nick }} - 8BitJelly</Title>
		</Head>

        <div>
            <Menu />
        </div>

        <div>
            <div class="pt-12 pb-36 flex justify-center">
		
                <div class="max-w-[29rem] relative pb-24 specifillacy_box border-2 border-pink-600 bg-pink-800/30 rounded-xl py-6 px-8">
                    <nuxt-img :src="'https://panel.8bitjelly.com'+osoba.data[0].attributes.Avatar.data.attributes.url" loading="lazy" alt="Image" class="max-w-[12rem] object-contain rounded-xl" />
                    <div class="mt-4 text-white/90">
                        <p class="text-2xl font-semibold" >{{ osoba.data[0].attributes.Nick }}</p>
                        <p class="text-xl font-semibold text-primary mb-4">{{ osoba.data[0].attributes.Stanowisko }}</p>
                        <p class="text-white/90" >{{ osoba.data[0].attributes.Opis }}</p>
        
                        <div class="mt-4 flex gap-8 items-end justify-center absolute w-full bottom-4 left-0">
                            <a v-if="osoba.data[0].attributes.Linkedin" :href="osoba.data[0].attributes.Linkedin" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/linkedin.svg" alt="">
                            </a>    
                            <a v-if="osoba.data[0].attributes.Instagram" :href="osoba.data[0].attributes.Instagram" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/instagram.svg" alt="">
                            </a>
                            <a v-if="osoba.data[0].attributes.GitHub" :href="osoba.data[0].attributes.GitHub" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/github.svg" alt="">
                            </a>
                            <a v-if="osoba.data[0].attributes.Website" :href="osoba.data[0].attributes.Website" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/globe.svg" alt="">
                            </a>
                            <a v-if="osoba.data[0].attributes.XTwitter" :href="osoba.data[0].attributes.XTwitter" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6 py-1" src="/icons/X.svg" alt="">
                            </a>
                            <a v-if="osoba.data[0].attributes.TikTok" :href="osoba.data[0].attributes.TikTok" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/tiktok.svg" alt="">
                            </a>
                            <a v-if="osoba.data[0].attributes.Facebook" :href="osoba.data[0].attributes.Facebook" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/facebook.svg" alt="">
                            </a>
                            <a v-if="osoba.data[0].attributes.Itchio" :href="osoba.data[0].attributes.Itchio" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/itchio.svg" alt="">
                            </a>
                            <a v-if="osoba.data[0].attributes.Artstation" :href="osoba.data[0].attributes.Artstation" class="p-2 bg-primary/20 rounded-lg" target="_blank">
                                <img class="h-6" src="/icons/artstation.svg" alt="">
                            </a>
                        </div>

                    </div>
                </div>
            </div>
        </div>

        <div class="fixed bottom-2 right-2 flex gap-2">
            <label for="lang" class="text-black/90 text-sm">Select language:</label>
            <select id="lang" v-model="locale" class="bg-primary/80 rounded-lg text-white px-2 z-50">
                <option class="" value="en">EN</option>
                <option class="" value="pl">PL</option>
            </select>
        </div>
    </div>
</template>


<script lang="ts" setup>
const route = useRoute()

const { locale } = useI18n()

const osoba = ref()
const lang = ref(locale.value)


const fetchUser = async () => {
    const { data, pending } = await useFetch(
        `https://panel.8bitjelly.com/api/osobies?populate=Avatar&locale=${lang.value}&filters[Nick][$eq]=${route.params.user}`
    )
    osoba.value = data.value

}

await fetchUser();

watch(locale, (newLocale, oldLocale) => {
    lang.value = newLocale

    fetchUser()

})

</script>