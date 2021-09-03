<template>
  <div class="home">
    <div class="home-text">
      <vuescroll>
        <img src="../assets/logo.png" width="250" /><br />
        A club of 101 unique Nerd Faces<br />
        Imagined by an AI for your next theme night.<br />
        --<br />
        <span class="title-drop">Drop party</span><br />06th September at 06:00
        CEST<br />
        <a href="https://twitter.com/Nerd_Face_NFT/"
          ><b-button type="is-danger">JOIN THE CLUB</b-button></a
        >
      </vuescroll>
    </div>
    <div class="home-images">
      <vuescroll>
        <img
          v-for="i in indexes"
          width="20%"
          style="float: left"
          v-bind:key="i"
          :src="'/gen_zero/pixel_nerdface_' + i + '.png'"
        />
      </vuescroll>
    </div>
  </div>
</template>
<style>
body,
html {
  background: #fff952;
}
</style>

<script>
import Web3 from "web3";
import vuescroll from "vuescroll";

export default {
  components: {
    vuescroll,
  },
  data() {
    return {
      selected_network: "",
      account: "",
      web3: "",
      balance: 0,
      indexes: [],
    };
  },
  methods: {
    async connect() {
      const app = this;
      if (window.ethereum) {
        // Check if network is desired one
        app.selected_network = await app.web3.eth.net.getId();
        // Request accounts
        await window.ethereum.send("eth_requestAccounts");
        // Read accounts
        const accounts = await app.web3.eth.getAccounts();
        if (accounts[0] !== undefined) {
          app.account = accounts[0];
          // Take balance
          const balance = await app.web3.eth.getBalance(accounts[0]);
          app.balance = parseFloat(
            app.web3.utils.fromWei(balance, "ether")
          ).toFixed(10);
          localStorage.setItem("connected", app.account);
        }
      } else {
        alert("Please install Metamask");
      }
    },
    async disconnect() {
      const app = this;
      localStorage.removeItem("connected");
      app.account = "";
      app.balance = 0;
      location.reload();
    },
    async switchNetwork(what) {
      const app = this;
      if (what === "polygon") {
        await window.ethereum.request({
          method: "wallet_addEthereumChain",
          params: [
            {
              chainId: "0x89",
              chainName: "Polygon",
              rpcUrls: ["https://rpc-mainnet.matic.network"],
              nativeCurrency: {
                name: "MATIC",
                symbol: "MATIC",
                decimals: 18,
              },
              blockExplorerUrls: ["https://polygonscan.com/"],
            },
          ],
        });
      } else if (what === "mumbai") {
        await window.ethereum.request({
          method: "wallet_addEthereumChain",
          params: [
            {
              chainId: "0x13881",
              chainName: "Mumbai",
              rpcUrls: ["https://rpc-mumbai.matic.today"],
              nativeCurrency: {
                name: "MATIC",
                symbol: "MATIC",
                decimals: 18,
              },
              blockExplorerUrls: ["https://mumbai.polygonscan.com/"],
            },
          ],
        });
      }
      app.connect();
    },
    refreshImages() {
      const app = this;
      app.indexes = [];
      while (app.indexes.length < 80) {
        let index = Math.floor(Math.random() * 80 + 1);
        let padded = app.pad(index, 3);
        if (app.indexes.indexOf(padded) === -1) {
          app.indexes.push(padded);
        }
      }
    },
    pad(n, width, z) {
      z = z || "0";
      n = n + "";
      return n.length >= width
        ? n
        : new Array(width - n.length + 1).join(z) + n;
    },
  },
  async mounted() {
    const app = this;
    if (window.ethereum) {
      app.web3 = await new Web3(window.ethereum);
      const accounts = await app.web3.eth.getAccounts();
      if (accounts.length > 0) {
        if (accounts[0] === localStorage.getItem("connected")) {
          const balance = await app.web3.eth.getBalance(accounts[0]);
          app.account = accounts[0];
          app.balance = parseFloat(
            app.web3.utils.fromWei(balance, "ether")
          ).toFixed(10);
        }
      }
    }
    app.refreshImages();
    setInterval(function () {
      app.refreshImages();
    }, 100);
  },
};
</script>
