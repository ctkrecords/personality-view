<template>
  <div id="app" class="mt-3 text-center">
    <PersonalityComponent
      msg="Bienvenido a Personality API" 
      msg2="Por favor ingresa el nombre de un usuario de twitter:"
    />
  </div>
</template>

<script>
import PersonalityComponent from './components/PersonalityComponent.vue'

export default {
  name: 'App',
  components: {
    PersonalityComponent
  }
}
</script>

<style>

</style>
