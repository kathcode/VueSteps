<template>
  <div class="hello">
    <h2>Hola! por favor responda a las siguientes <br>preguntas para generarle un diagnostico.</h2>
    <hr>
    <!-- computador.enciende ? -->
    <div v-if="steps.estado">
      <h2>{{ steps.mensaje }}</h2>
      <button class="btn" v-on:click="say(true, steps, 'true1')">Si enciende</button>
      <button class="btn" v-on:click="say(true, steps, 'false1')">No enciende</button>
    </div>

    <!-- computador.enciende.true -->
    <div v-if="steps.true1.estado">
      <h2>{{ steps.true1.mensaje }} </h2>
      <button class="btn" v-on:click="say(true, steps.true1, 'true2')">Si se reinica</button>
      <button class="btn" v-on:click="say(true, steps.true1, 'false2')">No se reinicia</button>
    </div>

    <!-- computador.enciende.false ? -->
    <div v-if="steps.false1.estado">
      <h2>{{ steps.false1.mensaje }}</h2>
      <button class="btn" v-on:click="say(true, steps.false1, 'true2')">Si esta conectado</button>
      <button class="btn" v-on:click="say(true, steps.false1, 'false2')">No esta conectado</button>
    </div>

    <!-- computador.conectado.true ? -->
    <div v-if="steps.false1.true2.estado">
      <h2>{{ steps.false1.true2.mensaje }}</h2>
      <button class="btn" v-on:click="say(true, steps.false1.true2, 'true3')">Si tiene corriente</button>
      <button class="btn" v-on:click="say(true, steps.false1.true2, 'false3')">No tiene corriente</button>
    </div>

    <!-- computador.conectado.false ? -->
    <div v-if="steps.false1.false2.estado">
      <h2>{{ steps.false1.false2.mensaje }} - {{steps.false1.true2.id}}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>

    <!-- sin corriente ? -->
    <div v-if="steps.false1.true2.false3.estado">
      <h2>{{ steps.false1.true2.false3.mensaje }}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>


    <!-- COn corriente ? -->
    <div v-if="steps.false1.true2.true3.estado">
      <h2>{{ steps.false1.true2.true3.mensaje }} </h2>
      <button class="btn" v-on:click="say(true, steps.false1.true2.true3, 'true4')">Si enciende el monitor</button>
      <button class="btn" v-on:click="say(true, steps.false1.true2.true3, 'false4')">No enciende el monitor</button>
    </div>

    <!-- No enciende monitor -->
    <div v-if="steps.false1.true2.true3.false4.estado">
      <h2>{{ steps.false1.true2.true3.false4.mensaje }} </h2>
    </div>

    <!-- Fuente de poder -->
    <div v-if="steps.false1.true2.true3.true4.estado">
      <h2>{{ steps.false1.true2.true3.true4.mensaje }} </h2>
      <button class="btn" v-on:click="say(true, steps.false1.true2.true3.true4, 'true5')">Fuente de poder bien</button>
      <button class="btn" v-on:click="say(true, steps.false1.true2.true3.true4, 'false5')">Fuente de poder mal</button>
    </div>

    <!-- Fuente de poder mal -->
    <div v-if="steps.false1.true2.true3.true4.false5.estado">
      <h2>{{ steps.false1.true2.true3.true4.false5.mensaje }} </h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>

    <!-- Fuente de poder bien -->
    <div v-if="steps.false1.true2.true3.true4.true5.estado">
      <h2>{{ steps.false1.true2.true3.true4.true5.mensaje }} </h2>
      <button class="btn" v-on:click="say(true, steps.false1.true2.true3.true4.true5, 'true6')">Perifericos bien</button>
      <button class="btn" v-on:click="say(true, steps.false1.true2.true3.true4.true5, 'false6')">Perifericos mal</button>
    </div>

    <!-- Perifericos bien -->
    <div v-if="steps.false1.true2.true3.true4.true5.true6.estado">
      <h2>{{ steps.false1.true2.true3.true4.true5.true6.mensaje }}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>

    <!-- Perifericos mal -->
    <div v-if="steps.false1.true2.true3.true4.true5.false6.estado">
      <h2>{{ steps.false1.true2.true3.true4.true5.false6.mensaje }}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>


    <!-- computador.reinicio.true -->
    <div v-if="steps.true1.true2.estado">
      <h2>{{ steps.true1.true2.mensaje }}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>

    <!-- computador.reinicio.false -->
    <div v-if="steps.true1.false2.estado">
      <h1>{{ steps.true1.false2.mensaje }} </h1>
      <button class="btn" v-on:click="say(true, steps.true1.false2, 'true3')">Si esta lento</button>
      <button class="btn" v-on:click="say(true, steps.true1.false2, 'false3')">No esta lento</button>
    </div>

    <!-- lento -->
    <div v-if="steps.true1.false2.true3.estado">
      <h2>{{ steps.true1.false2.true3.mensaje }}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>

    <!-- no lento -->
    <div v-if="steps.true1.false2.false3.estado">
      <h2>{{ steps.true1.false2.false3.mensaje }}</h2>
      <button class="btn" v-on:click="say(true, steps.true1.false2.false3, 'true4')">Si hay error</button>
      <button class="btn" v-on:click="say(true, steps.true1.false2.false3, 'false4')">No hay errores</button>
    </div>

    <!-- Con error -->
    <div v-if="steps.true1.false2.false3.true4.estado">
      <h2>{{ steps.true1.false2.false3.true4.mensaje }}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
    </div>

    <!-- Con error -->
    <div v-if="steps.true1.false2.false3.false4.estado">
      <h2>{{ steps.true1.false2.false3.false4.mensaje }}</h2>
      <button class="btn" v-on:click="recharge()">Inicio</button>
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
            mensaje: 'Diagnostico: Revisar e hardware, el Sistema operativo, y el disco duro',
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
            mensaje: '¿Tiene corriente?',
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
                  mensaje: 'Verificar la menoria y la board',
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
            id: 'verifique_conectiv',
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
body {
  padding: 20px;
}
.hello {
  padding: 30px;
}
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
div {
  margin: 40px 0px;
}
a {
  color: #42b983;
}
button {
  cursor: pointer;
}
button:focus {
    background-color: #4196d0;
}

button:active {
    background-color: #4196d0;
}
</style>
