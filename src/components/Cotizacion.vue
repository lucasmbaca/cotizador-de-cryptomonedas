<script setup>
defineProps({
    cotizacion:{
        type:Object,
        required:true
    }
})
</script>


<template>
    <div 
        class="contenedor-resultado"
    >
        <h2>Cotizacion</h2>
        <div class="resultado">
            <img :src="'http://cryptocompare.com/' + cotizacion.IMAGEURL" alt="crypo">
            <div>
            <p>El precio es de: <span>{{cotizacion.PRICE}}</span></p>
            <p>Precio mas alto del dia: <span>{{ cotizacion.HIGHDAY }}</span></p>
            <p>Precio mas bajo del dia: <span>{{ cotizacion.LOWDAY }}</span></p>
            <p>Variacion ultimas 24hrs: <span>{{ cotizacion.CHANGEPCT24HOUR }}%</span></p>
            <p>Ultima actualizacion: <span>{{ cotizacion.LASTUPDATE }}</span></p>
            </div>
        </div>
    </div>
</template>