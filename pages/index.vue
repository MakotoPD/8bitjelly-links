<template>
    <div>

        <Head>
			<Title>8BitJelly</Title>
		</Head>
    </div>
</template>


<script lang="ts" setup>

onMounted(() => {
    const router = useRouter()

        router.push('/someone')
})
</script>