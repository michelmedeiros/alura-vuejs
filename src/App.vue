
<template>
  
  <div id="app" class="corpo"> 
    <meu-menu :rotas="routes"/>
    <transition name="pagina">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>

import { routes } from './routes'
import MeuMenu from './components/shared/MeuMenu.vue'

export default {
  
  components: {
    MeuMenu
  },

  data () {
    return {
      routes
    }
  }
}

</script>

<style>

  .corpo {
    font-family: Arial, Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }

  .pagina-enter-active, .pagina-leave-active {
    transition: opacity .3s
  }

  .pagina-enter, .pagina-leave-active {
    opacity: 0
  }

</style>
