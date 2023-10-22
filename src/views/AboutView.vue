<script>
export default {
  // Properties returned from data() become reactive state
  // and will be exposed on `this`.
  data() {
    return {
      count: 0,
      pokemons: [],
      inputText: "test"
    }
  },

  // Methods are functions that mutate state and trigger updates.
  // They can be bound as event handlers in templates.
  methods: {
    increment() {
      this.count++
    },
    decrement() {
      this.count--
    },
    clickPokemon(name, e){
      console.log("pokemon name", name, event)
    },
    renderMethod(){
      console.log("render")
    }
  },

  watch: {
    'this.$count': {
      handler() {
        this.renderMethod()
      }
    }
  },

  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  async mounted() {
    const data = await fetch('https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0')
    const res = await data.json()
    this.pokemons = res.results
  }
}
</script>

<template>
  <div class="about">
    <!-- <h1>This is an about page</h1> -->
    <div style="display: flex; gap: 40px;">
      <div>
        <button @click="decrement">Decrement</button>
        <div style="margin: 30px">{{ count }}</div>
        <button @click="increment">Increment</button>
      </div>
      <div>
        <button v-for="pokemon in pokemons" :key="pokemon.name" @click="clickPokemon(pokemon.name, $event)"> {{ pokemon.name }}</button>
      </div>
      <div>
        <input type="" v-model="inputText" />
      </div>
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
