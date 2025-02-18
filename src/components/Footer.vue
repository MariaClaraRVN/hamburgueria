<template>
    <div id="footer">
        <p>FAÇA O SEU HAMBÚRGUER &copy; 2025</p>
        <p>Todos os direitos reservados.</p>
    </div>
</template>

<script>
export default{
    name: 'Footer'
}
</script>

<style scoped>
#footer{
    height: 200px;
    background-color: #222;
    border-top: 4px solid #111;
    color: #fcba03;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
    flex-direction: column;
}
</style>