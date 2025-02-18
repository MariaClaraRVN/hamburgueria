<template>
    <div id="main-banner">

    </div>
</template>

<script>
export default{
    name: 'Banner'
}
</script>

<style scoped>
#main-banner{
    background-image: url("/public/img/Banner.jpg");
    background-size: cover;
    background-position: center;
    width: 100%;
    height: 600px;
}

@media (max-width: 780px) {
    #main-banner {
        height: auto;
        min-height: 160px;
        max-height: 300px;
    }
}


</style>