
<template>
  <div id="home"> 
    <h1 class="centralizado">{{ mensagem }}</h1>
    <input type="search" @input="filtro = $event.target.value" class="filtro" placeholder="Digite o título da foto">
    <ul id="#fotos" class="lista-fotos">
      <li v-for="foto of fotosComFiltro" class="lista-fotos-item">
        <painel :titulo="foto.titulo">
            <imagem-responsiva :src="foto.url" :alt="foto.titulo"/>
            <botao 
              :confirmacao="false" 
              tipo="button" 
              rotulo="Excluir" 
              estilo="perigo"
              @botaoAtivado="remove(foto)"/>
        </painel>
      </li>
    </ul>
  </div>
</template>

<script>

import Painel from '../shared/Painel.vue'
import ImagemResponsiva from '../shared/ImagemResponsiva.vue'
import Botao from '../shared/Botao.vue'
export default {
  
  components: {
    Painel, ImagemResponsiva, Botao
  },

  data () {
    return {
      mensagem : 'AluraPic',
      fotos: [],
      filtro: ''
    }
  },

  methods: {
    remove(foto) {
      alert('Foto removida: ' + foto.titulo);
    }
  },

  computed: {
    fotosComFiltro() {
      if(this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      }else {
        return this.fotos;
      }
    }
  },

  created() {
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}

</script>

<style>
  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    display : block;
    width: 100%;
  }

</style>
