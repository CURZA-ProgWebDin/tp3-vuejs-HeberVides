<template>
  <div ref="box" class="contenedorListas">
  <p v-if="cargando" class="mensajeCargando">Cargando...</p>
    <!-- INSTANCIA 1 -->
    <div class="bloqueInstancia">
      <h2>Instancia 1: Header + Body + Footer</h2>
      <div class="lista">
        <TarjetaProducto v-for="p in productos" :key="p.id">

          <!-- HEADER -->
          <template #header>
            <h3>{{ p.nombre }}</h3>
            <small>{{ p.categoria }}</small>
          </template>

          <!-- BODY -->
          <template #body="{ expandida }">
            <p>Precio: {{ p.precio }}</p>
            <p v-if="expandida">Stock: {{ p.stock }}</p>
          </template>
                  
          <!-- FOOTER -->
          <template #footer="{ toggleExpandir, expandida }">
            <button @click="toggleExpandir">
              {{ expandida ? 'Mostrar Menos' : 'Stock Disponible' }}
            </button>
            <button>Comprar</button>
            <a href="#">Más Info</a>
          </template>
        </TarjetaProducto>
      </div>
    </div>

    <!-- INSTANCIA 2 -->
    <div class="bloqueInstancia">
      <h2>Instancia 2: Header + Body</h2>
      <div class="lista">
        <TarjetaProducto v-for="p in productos" :key="p.id">

          <!-- HEADER -->
          <template #header>
            <h3>{{ p.nombre }}</h3>
            <small>{{ p.categoria }}</small>
          </template>

          <!-- BODY -->
          <!-- Como se necesita mostrar el stock en el body, se le agrega el boton. --> 
          <template #body="{ expandida, toggleExpandir }">
            <button @click="toggleExpandir">{{ expandida ? 'Ocultar' : 'Ver Stock' }}</button>
            <p v-if="expandida">Stock: {{ p.stock }}</p>
          </template>
        </TarjetaProducto>
      </div>
    </div>

    <!-- INSTANCIA 3 -->
    <div class="bloqueInstancia">
      <h2>Instancia 3: Header + Footer</h2>
      <div class="lista">
        <TarjetaProducto v-for="p in productos" :key="p.id">

          <!-- HEADER -->
          <template #header>
            <h3>{{ p.nombre }}</h3>
            <p> {{ p.categoria }}</p>
          </template>

          <!-- FOOTER -->
          <template #footer>
            <a href="#">Enlace Productos Similares</a>
            <p></p>
          </template>
        </TarjetaProducto>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, onMounted, onUpdated, onBeforeUnmount, useTemplateRef } from 'vue'
import TarjetaProducto from './TarjetaProducto.vue'

const props = defineProps({
  productos: {type:Array, required: true}
})

const box = useTemplateRef('box')
const cargando = ref(false)
let timer = null

function esperar(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function cargarProductos() {
  cargando.value = true
  await esperar(800)  
  cargando.value = false
}

onMounted(() => {
  cargarProductos()
  timer = setInterval(cargarProductos, 30000)
})

onUpdated(() => {
  if (box.value) {
    box.value.scrollTop = box.value.scrollHeight
  }
})

onBeforeUnmount(() => {
  clearInterval(timer)
  console.log('ListaProductos desmontado — polling detenido')
})
</script>

<style scoped>
.contenedorListas {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.bloqueInstancia {
  padding: 15px;
  border-radius: 8px;
  background-color: #ffa0a0;
}

.lista {
  max-height: 300px;
  overflow-y: auto;
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  background-color: #ffffff;
  border-radius: 10px;
}

.mensajeCargando{

  color: #00eeff; 
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;

}
</style>