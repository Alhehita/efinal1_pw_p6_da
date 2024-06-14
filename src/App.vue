<template>
  <div class="juego">
    <div v-if="!finJuego" class="info">
      <p>Puntaje: {{ puntaje }}</p>
      <p>Intentos: {{ intentos }}</p>
    </div>

    <div v-if="!finJuego" class="pokemonsImg">
      <Imagen
        :imagen="pokemonsImg[0].imagen"
        :nombre="pokemonsImg[0].nombre"
        :class="{ inicio: !juegoIniciado }"
      />

      <Imagen
        :imagen="pokemonsImg[1].imagen"
        :nombre="pokemonsImg[1].nombre"
        :class="{inicio: !juegoIniciado}"
      />

      <Imagen
        :imagen="pokemonsImg[2].imagen"
        :nombre="pokemonsImg[2].nombre"
        :class="{inicio: !juegoIniciado}"
      />
    </div>

    <button v-if="!finJuego" @click="jugar">JUGAR</button>
    <div v-if="finJuego" class="mensaje">
      <p v-if="puntaje >= 10" class="mensajePuntaje">Puntaje: {{ puntaje }}</p>
      <img
        v-if="puntaje >= 10"
        src="https://via.placeholder.com/250"
        alt="No se pudo cargar la imagen"
        class="imgCarga"
      />
      <p :class="claseMensaje">{{ mensaje }}</p>
      <button @click="reiniciarJuego">Nuevo Juego</button>
    </div>
  </div>
</template>

<script>
import Imagen from "./components/Imagen.vue";

export default {
  components: {
    Imagen,
  },
  data() {
    return {
      pokemonsImg: [
        { imagen: "https://via.placeholder.com/250", nombre: "XXXXX" },
        { imagen: "https://via.placeholder.com/250", nombre: "XXXXX" },
        { imagen: "https://via.placeholder.com/250", nombre: "XXXXX" },
      ],
      pokemon: [1, 2, 3, 4, 5],
      puntaje: 0,
      intentos: 0,
      mensaje: "",
      finJuego: false,
      inicioJuego: false,
    };
  },
  computed: {
    claseMensaje() {
      return this.puntaje >= 10 ? "gana" : "pierde";
    },
  },
  methods: {
    async jugar() {
      if (this.finJuego) return;

      this.inicioJuego= true;
      const pokemonesSeleccionados = [];

      for (let i = 0; i < 3; i++) {
        const indiceAleatorio = Math.floor(
          Math.random() * this.pokemon.length
        );

        const idPokemon = this.pokemon[1,12,23,34,45];
        const respuesta = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${1}`
        );
        const datos = await respuesta.json();
        pokemonesSeleccionados.push({
          imagen: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${1}.svg`,
          nombre: datos.name,
        });

        const respuesta1 = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${12}`
        );
        const datos1 = await respuesta1.json();
        pokemonesSeleccionados.push({
          imagen: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${12}.svg`,
          nombre: datos1.name,
        });
        
        const respuesta2 = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${23}`
        );
        const datos2 = await respuesta2.json();
        pokemonesSeleccionados.push({
          imagen: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${23}.svg`,
          nombre: datos2.name,
        });
        
        const respuesta3 = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${34}`
        );
        const datos3 = await respuesta3.json();
        pokemonesSeleccionados.push({
          imagen: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${34}.svg`,
          nombre: datos3.name,
        });
        
        const respuesta4 = await fetch(
          `https://pokeapi.co/api/v2/pokemon/${45}`
        );
        const datos4 = await respuesta4.json();
        pokemonesSeleccionados.push({
          imagen: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${45}.svg`,
          nombre: datos4.name,
        });
      }

      this.pokemonsImg = pokemonesSeleccionados;
      this.actualizarPuntaje(pokemonesSeleccionados);
      this.intentos++;

      if (this.intentos >= 5 || this.puntaje >= 10) {
        this.finJuego = true;
        this.mensaje =
          this.puntaje >= 10
            ? `Felicitaciones has ganado un premio de $10.000,00`
            : `Has utilizado tus 5 intentos. El juego ha terminado, intentalo nuevamente`;
      }
    },
    actualizarPuntaje(pokemonesSeleccionados) {
      const nombres = pokemonesSeleccionados.map((pokemon) => pokemon.nombre);
      const nombresUnicos = [...new Set(nombres)];
      if (nombresUnicos.length === 1) {
        this.puntaje += 5;
      } else if (nombresUnicos.length === 2) {
        this.puntaje += 2;
      } else {
        this.puntaje +=0;
      }
    },
    reiniciarJuego() {
      this.pokemonsImg = [
        { imagen: "https://via.placeholder.com/250", nombre: "XXXXX" },
        { imagen: "https://via.placeholder.com/250", nombre: "XXXXX" },
        { imagen: "https://via.placeholder.com/250", nombre: "XXXXX" },
      ];
      this.puntaje = 0;
      this.intentos = 0;
      this.mensaje = "";
      this.finJuego = false;
      this.inicioJuego= false;
    },
  },
};
</script>

<style >
.juego {
  text-align: center;
}

.info {
  display: flex;
  justify-content: space-evenly;
  padding: 0 20px;
}

.pokemonsImg {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-left: 20px;

}

button {
  margin-top: 20px;
  border: solid black 3px;
  padding: 5px;
  width: 75px;
}

.mensaje {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.mensajePuntaje {
  font-size: 1.5px;
  margin-bottom: 10px;
  color: blue;
}

.imgCarga {
  margin-top: 10px;
  width: 100px;
  height: auto;
  object-fit: cover;
}

.gana {
  color: blue;
  margin-top: 10px;
}

.pierde {
  color: red;
  margin-top: 10px;
}

.pokemon-PokemonImg {
  text-align: center;
}

.pokemon-PokemonImg img {
  width: 100px;
  height: 100px;
}
</style>
