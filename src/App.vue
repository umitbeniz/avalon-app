<template>
  <div class="app" id="app">
    <div class="container mx-auto">
      <div class="header-container">
        <p class="header gradient-text">
          <a href="https://www.avaxmart.com"><img class="logo" src="@/assets/logo2.png" alt="Avalon logo" /></a> 
        </p>
        <p class="sub-text">NFT Game On Avalanche Blockchain</p>
        <div class="connect-wallet-container" v-if="!account">
          <img class="banner" src="@/assets/banner.gif" alt="Avalon logo" />
          <button class="cta-button connect-wallet-button" @click="connect">
            Connect Wallet
          </button>
        </div>
        <select-character v-else-if="account && !characterNFT" />
        <stake v-else-if="account && characterNFT" />
      </div>
      <div class="footer-container">
        <a class="footer-text">Built with ❤️ Avalon Team</a>
      </div>
    </div>
  </div>
</template>

<script>
import SelectCharacter from "./components/SelectCharacter.vue";
import Stake from "./components/Stake.vue";
export default {
  name: "App",
  data() {
    return {};
  },
  methods: {
    async connect() {
      await this.$store.dispatch("connect", 1);
    },
  },
  async mounted() {
    await this.$store.dispatch("connect");
  },
  computed: {
    account() {
      return this.$store.getters.account;
    },
    mining() {
      return this.$store.getters.mining;
    },
    characterNFT() {
      return this.$store.getters.characterNFT;
    },
  },
  components: {
    SelectCharacter,
    Stake,
  },
};
</script>

<style>
.logo {
  max-width: 250px;
  display: initial;
  margin-top: -35px;
}

.banner {
  width: auto;
  height: auto;
}

.app {
  height: 100vh;
  background-color: rgb(53, 100, 131);
  overflow: scroll;
  text-align: center;
}

.container {
  height: 100%;
  background-color: rgb(53, 100, 131);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.header-container {
  padding-top: 30px;
}

.header {
  margin: 0;
  font-size: 50px;
  font-weight: bold;
  color: white;
}

.sub-text {
  font-size: 25px;
  color: white;
}

.content-container {
  background-color: #a200d6;
}

.cta-button {
  height: 45px;
  border: 0;
  width: auto;
  padding-left: 40px;
  padding-right: 40px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  color: white;
}

.connect-wallet-container {
  display: flex;
  flex-direction: column;
  margin: auto;
  max-width: 550px;
}

.connect-wallet-container img {
  padding-bottom: 20px;
}

.connect-wallet-button {
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
}

.mint-button {
  background: -webkit-linear-gradient(left, #a200d6, #ff6fdf);
  background-size: 200% 200%;
  animation: gradient-animation 4s ease infinite;
  margin-right: 15px;
}

.mint-count {
  color: white;
  font-size: 18px;
  font-weight: bold;
}

.footer-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 30px;
}

.twitter-logo {
  width: 35px;
  height: 35px;
}

.footer-text {
  color: white;
  font-size: 16px;
  font-weight: bold;
}

/* KeyFrames */
@-webkit-keyframes gradient-animation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
@-moz-keyframes gradient-animation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
@keyframes gradient-animation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
