<template>
    <div id="app">
        <HeaderPage/>
        <Nuxt/>
        <FooterPage/>
    </div>
</template>

<script>
// Memanggil component sesuai lokasi masing - masing file
import HeaderPage from "@/components/HeaderPage.vue"
import FooterPage from "@/components/FooterPage.vue"
export default {
// Dideklarasikan agar dapat diakses oleh template
components: {HeaderPage,FooterPage}
}
</script>

<style>

</style>