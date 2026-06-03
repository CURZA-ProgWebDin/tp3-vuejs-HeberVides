<template>
  <div class="panelPestanas">
    <div class="botonesTabs">
      <button @click="tabActivo = 'TabTodos'">Todos</button>
      <button @click="tabActivo = 'TabElectronica'">Electrónica</button>
      <button @click="tabActivo = 'TabPerifericos'">Periféricos</button>
    </div>

    <div class="contenedorTabs">
      <!-- contenedor de la izquierda -->
      <div class="bloquesTab">
        <h1 class="titulo">Sin KeepAlive</h1>
        <component :is="tabs[tabActivo]" />
      </div>

      <!-- contenedor de la derecha -->
      <div class="bloquesTab">
        <h1 class="titulo">Con KeepAlive</h1>
        <KeepAlive>
          <component :is="tabs[tabActivo]" />
        </KeepAlive>
      </div>
    </div>
  </div>

<!-- 
  Respondé esta pregunta en un comentario dentro de PanelPestanas.vue: ¿En qué situación conviene usar KeepAlive y en cuál no?
    Conviene => cuando queremos mantener el estado de los datos de un formulario o escrolls por ejemplo. 
    NO conviene => si consume mucha memoria o si deseamos reiniciar un componente.
-->

</template>

<script setup>
import { ref } from 'vue'
import TabTodos from './components/tabs/TabTodos.vue'
import TabElectronica from './components/tabs/TabElectronica.vue'
import TabPerifericos from './components/tabs/TabPerifericos.vue'

const tabActivo = ref('TabTodos')

const tabs = {
  TabTodos,
  TabElectronica,
  TabPerifericos
}
</script>

<style scoped>
.panelPestanas {
  display: flex;
  flex-direction: column; 
  gap: 20px;
}

.botonesTabs {
  display: flex;
  justify-content: center;
  gap: 12px;
}

.botonesTabs button {
  background-color: #ff1f44;
}

.botonesTabs button:hover{
  background-color: #009ffc;
}

.contenedorTabs {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: flex-start;
  align-items: center;
  gap: 40px;
  width: 90%;
  overflow: visible;
}

.bloquesTab {
  flex: 1;
  justify-content: center; 
  min-width: 100%;
}

.titulo {
  font-size: 2rem;
  color: #fa3142;
  text-shadow: 2px 2px 4px rgba(0, 247, 255, 0.623);
  margin-bottom: 10px;
  text-align: center;
}
</style>