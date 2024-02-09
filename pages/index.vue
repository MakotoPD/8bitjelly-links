<template>
    <div>

        <Head>
			<Title>8BitJelly - </Title>
		</Head>

        <div>
            <Menu />
        </div>

        <div>
            <p>{{ osoba.Nick }}</p>
        </div>
    </div>
</template>


<script lang="ts" setup>
const route = useRoute()

console.log(route.params)


const { locale } = useI18n()

const osoba = ref()
const lang = ref(locale.value)
const nickname = ref('MakotoPD')


const fetchUser = async () => {
    const { data, pending } = await useFetch(
        `https://panel.8bitjelly.com/api/osobies?populate=Avatar&locale=${lang.value}&filters[Nick][$eq]=${nickname.value}`
    )
    osoba.value = data.value

    console.log(data.value)

}

await fetchUser();

osoba.value = osoba.value.data[0].attributes

watch(locale, (newLocale, oldLocale) => {
    lang.value = newLocale


    fetchUser()
})

</script>