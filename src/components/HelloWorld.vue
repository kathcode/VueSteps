<template>
  <div class="hello">

    <!-- computador.enciende -->
    <div v-if="steps.estado">
      <h1>{{ steps.mensaje }}</h1>
      <button class="btn" v-on:click="say(true, steps, 'true1')">Yes</button>
      <button class="btn" v-on:click="say(true, steps, 'false1')">No</button>
    </div>

    <!-- computador.enciende.true -->
    <div v-if="steps.true1.estado">
      <h1>{{ steps.true1.mensaje }}</h1>
      <button class="btn" v-on:click="say(true, steps.true1, 'true2')">Yes</button>
      <button class="btn" v-on:click="say(true, steps.false1, 'false2')">No</button>
    </div>

    <!-- computador.enciende.false -->
    <div v-if="steps.false1.estado">
      <h1>{{ steps.false1.mensaje }}</h1>
      <button class="btn" v-on:click="say(true, steps.true1.true2, 'true2')">Yes</button>
      <button class="btn" v-on:click="say(true, steps.false1.false2, 'false2')">No</button>
    </div>

    <!-- computador.reinicio.true -->
    <div v-if="steps.true1.true2.estado">
      <h1>{{ steps.true1.true2.mensaje }}</h1>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>

    <!-- computador.reinicio.false -->
    <div v-if="steps.false1.false2.estado">
      <h1>{{ steps.false1.false2.mensaje }}</h1>
      <button class="btn" v-on:click="say(true, steps.true1.true2.true3.true4, 'true4')">Yes</button>
      <button class="btn" v-on:click="say(true, steps.false1.false2.false3.false4, 'false4')">No</button>
    </div>

    <div v-if="mensaje_finalizar.state">{{ mensaje_finalizar.mensaje }}</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      mensaje_finalizar: { state: false, mensaje: "Ha finalizado tu diagnostico. Gracias" },
      steps: {
        id:'computador.enciende',
        mensaje: '¿El computador enciende?',
        estado: true,
        true1: {
          id: 'computador.enciende.true',
          mensaje: '¿El computador se esta reinicioando?',
          estado: false,
          true2: {
            id: 'computador.reinicio.true',
            mensaje: 'Revisar e hardware, el Sistema operativo, y el disco duro',
            estado: false,
          },
          false2: {
            id: 'computador.reinicio.false',
            mensaje: '¿Encuentra lento el computador?',
            estado: false,
            true3: {
              mensaje: 'Por favor verifique el sistema operativo',
              estado: false,
            },
            false3: {
              mensaje: '¿Presenta algún mensaje de error?',
              estado: false,
              true4: {
                mensaje: 'Verifique el sistema operativo',
                estado: false,
              },
              false4: {
                mensaje: 'Contactese con un tecnico de mantenimiento',
                estado: false,
             },
            },
          },
        },
        false1: {
          id: 'computador.enciende.false',
          mensaje: '¿Esta conectado?',
          estado: false,
          true2: {
            ensaje: '¿Tiene corriente?',
            estado: false,
            true3: {
              mensaje: '¿El monitor enciende?',
              estado: false,
              true4: {
                mensaje: '¿La fuente de poner enciende?',
                estado: false,
                true5: {
                  mensaje: '¿Tiene los perifericos conectados?',
                  estado: false,
                  true6: {
                    mensaje: 'Desconectar y volver a conectar',
                    estado: false,
                  },
                  false6: {
                    mensaje: 'Verificar RAM y disco duro',
                    estado: false,
                  },
                },
                false5: {
                  mensaje: 'Verificar la menoria y la boars',
                  estado: false,
                },
              },
              false4: {
                mensaje: 'Por favor cambie de monitor',
                estado: false,
              },
            },
            false3: {
              mensaje: 'Verifique su electricidad',
              estado: false,
            },
          },
          false2: {
            mensaje: 'Verifique su conectividad',
            estado: false,
          },
        },
      }
    }
  },
  methods: {
    say: function (estado, posicion, step) {
      debugger
      if (step === 'finaliza') {
        this.mensaje_finalizar.state = true;
      }
      posicion[step].estado = estado;
    },
    recharge: function () {
      location.reload();
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
  cursor: pointer;
}
</style>
