<template>
    <div class="mensagem">
        <p>{{ msg }}</p>
    </div>
</template>


<script>
export default{
    name: 'Message',
    props:{
        msg : String
    }
}
</script>

<style scoped>
.mensagem{
    color: #004085;
    background-color:#cce5ff ;
    border: 2px solid #88daff;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;

}
</style>