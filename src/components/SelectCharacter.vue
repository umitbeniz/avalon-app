<template>
  <div class="select-character-container">
    <h2 class="mt-5">Mint Your Character</h2>
    <div v-if="characters.length && !minting" class="character-grid">
      <div
        class="character-item cursor-pointer mt-10"
        :key="character.name"
        v-for="(character, index) in characters"
      >
        <div class="name-container">
          <p>{{ character.name }}</p>
        </div>
        <img :src="character.imageURI" :alt="character.name" />
        <button
          type="button"
          class="character-mint-button"
          @click="mintCharacterNFTAction(index)"
        >
          {{ `Mint ${character.name}` }}
        </button>
      </div>
    </div>
    <div class="loading" v-else>
      <div class="indicator">
        <loading-indicator />
        <p>Minting...</p>
      </div>
     
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      minting: false,
    };
  },
  components: {
  },
  methods: {
    async mintCharacterNFTAction(index) {
      if (this.minting) return;
      this.minting = true;
      await this.$store.dispatch("mintCharacterNFT", index);
      this.minting = false;
    },
  },
  async mounted() {
    this.minting = true;
    await this.$store.dispatch("getCharacters");
    this.minting = false;
  },
  computed: {
    characters() {
      return this.$store.getters.characters;
    },
  },
};
</script>

<style scoped>
.select-character-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: white;
}

.select-character-container .character-grid {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  grid-template-rows: repeat(auto-fit, minmax(300px, 1fr));
  grid-row-gap: 15px;
}

.character-grid .character-item {
  display: flex;
  flex-direction: column;
  position: relative;
  justify-self: center;
  align-self: center;
}

.character-item img {
  height: 300px;
  width: 350px;
  border-radius: 10px;
  object-fit: cover;
}

.character-item .name-container {
  position: absolute;
  background-color: #fd2236;
  border-radius: 5px;
  margin: 10px;
}

.character-item .name-container p {
  margin: 0;
  padding: 5px 10px 5px 10px;
  font-weight: bold;
}

.character-item .character-mint-button {
  /* position: absolute;
  bottom: 0;
  /* width: 100%; */
  height: 40px;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  border: none;
  cursor: pointer;
  /* background-color: rgb(32, 129, 226); */
  color: white;
  font-weight: bold;
  font-size: 16px; 

  background-image: linear-gradient(
    to right,
    #f36c77 0%,
    #e43d4b 21%,
    #fd2236 52%,
    #fd2236 52%,
    #fd2236 78%,
    #fd2236 100%
  );
  background-size: 200% 200%;
  animation: gradient-animation 4s ease infinite;
  background-color: #a200d6;

}




.select-character-container .loading {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 75px;
}

.select-character-container .loading .indicator {
  display: flex;
}

.select-character-container .loading .indicator p {
  font-weight: bold;
  font-size: 28px;
  padding-left: 5px;
}

.select-character-container .loading img {
  width: 450px;
  padding-top: 25px;
}
</style>