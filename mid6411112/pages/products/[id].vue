<template>
    <div>
        <Head>
            <Title>Online Catalog | {{ product.album }}</Title>
            <Meta name="description" :content="product.performer" />
        </Head>
        <ProductDetails :product="product" />
    </div>
</template>

<script setup>
    const { updated_time } = useRoute().params
    const uri = 'https://fuzik03.tetraserver.com/compactdisc_list' + updated_time

    // fetch singlle product
    const { data: product } = await useFetch(uri, { key: updated_time})

    if(!product.value) {
        throw createError({ statusCode: 404, statusMessage: 'Product not found'})
    }

    definePageMeta({
        layout:'products'
    })
    
</script>

<style scoped>

</style>