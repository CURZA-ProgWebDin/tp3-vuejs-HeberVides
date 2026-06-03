<template>
  <ListaProductos :productos="filtrados" />
</template>

<script setup>
import { productos } from '../../data/productos'
import ListaProductos from '../ListaProductos.vue'
import { onMounted, onUnmounted, onActivated, onDeactivated } from 'vue'

const filtrados = productos.filter(p => p.categoria === 'Electrónica')

onMounted(() => console.log('TabElectronica — montado'))
onUnmounted(() => console.log('TabElectronica — desmontado'))
onActivated(() => console.log('TabElectronica — activado'))
onDeactivated(() => console.log('TabElectronica — desactivado'))
</script>