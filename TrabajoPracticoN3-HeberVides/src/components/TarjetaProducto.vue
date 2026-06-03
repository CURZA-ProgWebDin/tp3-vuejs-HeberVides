<template>
  <div class="tarjeta">
    
    <div class="header">
      <slot name="header"></slot>
    </div>

    <div class="body">
      <slot name="body" :expandida="expandida" :toggleExpandir="toggleExpandir"></slot>
    </div>

    <div class="footer">
      <slot name="footer" :expandida="expandida" :toggleExpandir="toggleExpandir">
        <p>Sin acciones disponibles</p>
      </slot>
    </div>

  </div>
</template>

<!--
#header — para el nombre y categoría del producto
#body — para el precio y stock 
#footer — para acciones (botones, links, etc.) (¡***!)

"El componente debe manejar internamente un estado booleano expandida (con ref) 
que indique si la tarjeta está expandida o no, y exponerlo al padre a través del slot #body:"

(¡***!) Ya que se pide que los botones y acciones deben ir en Footer, pero siendo el Body donde se tiene
que mostrar el precio/stock, se le pasa las mismas props al Body y Footer, para cuando se da click en el boton 
"stock disponible" en el Footer se pueda mostrar el stock en el Body.

POR ESTE MOTIVO ES QUE SE REPITE ":expandida="expandida" :toggleExpandir="toggleExpandir" EN AMBOS
-->

<script setup>
import { ref } from 'vue'

const expandida = ref(false)

function toggleExpandir() {
  expandida.value = !expandida.value
}
</script>

<style scoped>
.tarjeta {
  border: 1px solid #ff8787;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 10px;
  margin: 8px
}
</style>