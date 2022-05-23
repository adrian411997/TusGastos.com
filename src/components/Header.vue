<template>
    <header style="background-color: #3f3752">
        <nav class="navbar navbar-light">
            <div class="headers">
                <a class="navbar-brand" href="#">
                    <img v-bind:src="require('../assets/gastos.png')" alt="gastos" class="icono" style="width:80px;">
                </a>
                <h1 class="text-light">Visualizador de Gastos</h1>  
            </div>
        </nav>
    </header>
</template>
<script>
    export default {
        name: "Header",
    }
</script>
<style scoped>
    .headers{
        display: inline-flex;
        align-items: center;
    }
    .logout{
        text-align:right;
    }
    button{
        width: 50px;
        height: 50px;
    }
</style>