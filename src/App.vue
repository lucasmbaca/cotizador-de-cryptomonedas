<script setup>
  import {ref, reactive} from 'vue'

  import useCrypto from './composable/useCryto'

  import Cotizacion from './components/Cotizacion.vue'
  import Alerta from './components/Alerta.vue'
  import Cargador from './components/Cargador.vue'
  
  const { monedas, criptomonedas, cargando, cotizacion, obtenerCotizacion, mostrarResultado } = useCrypto()
  const error = ref('')

  const cotizar = reactive({
    moneda:'',
    criptomoneda:''
  })

  const cotizarCripto = () => {
    if(Object.values(cotizar).includes('')){
      error.value = 'todos los campos son obligatorios'
      return 
    }
    error.value = ''
    obtenerCotizacion(cotizar)
  }

</script>

<template>
  <div class="contenedor">
    <h1 class="titulo">Cotizador de <span>criptomonedas</span></h1>

    <div class="contenido">

      <Alerta
      v-if="error"
      >
      {{ error }}
      
      </Alerta>

      <form 
        class="formulario"
        @submit.prevent="cotizarCripto"
      >
        <div class="campo">
          <label for="moneda">Moneda:</label>
          <select 
            id="moneda"
            v-model="cotizar.moneda"
          >
            <option value="">-- seleccion --</option>
            <option 
              v-for="moneda in monedas"
              :value="moneda.codigo"
            >
              {{ moneda.texto }}
            </option>
          </select>
        </div>

        <div class="campo">
          <label for="cripto">Criptomonedas:</label>
          <select 
            id="cripto"
            v-model="cotizar.criptomoneda"
          >
            <option value="">-- seleccion --</option>
            <option 
              v-for="criptomoneda in criptomonedas"
              :value="criptomoneda.CoinInfo.Name"
            >
              {{ criptomoneda.CoinInfo.FullName }}
            </option>
          </select>
        </div>

        <input type="submit" value="cotizar">
      </form>

      <Cargador
        v-if="cargando"
      />
      <Cotizacion
        v-if="mostrarResultado"
        :cotizacion="cotizacion"
      />

    </div>
  </div>
</template>

