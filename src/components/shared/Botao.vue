
<template>
    <button @click="disparaAcao()" :class="estiloBotao" :type="tipo">{{ rotulo }}</button>
</template>

<script>
    export default {
        props: {
            tipo: {
                required: true,
                type: String
            },
            rotulo: {
                required: true,
                type: String
            },
            confirmacao: {
                required: false,
                type: Boolean
            },
            estilo: {
                required: false,
                type: String
            }
        },
            

        methods: {
            disparaAcao() {
                if(this.confirmacao) {
                    if(confirm('Confirma exclusão de foto?')) {
                        this.$emit('botaoAtivado');
                    }
                    return;
                }
                return this.$emit('botaoAtivado');
            }
        },

        computed: {

          estiloBotao() {
              if(this.estilo == 'padrao' || !this.estilo) return 'botao botao-padrao';
              if(this.estilo == 'perigo') return 'botao botao-perigo';
          }  
        }

    }
</script>

<style scoped>
    .botao {
        display: inline-block;
        padding: 10px;
        border-radius: 3px;
        margin: 10px;
        font-size: 1.2em;
    }

    .botao-perigo {
        background: firebrick;
        color: white;
    }

    .botao-padrao {
        background: darkcyan;
        color: white;
    }
</style>