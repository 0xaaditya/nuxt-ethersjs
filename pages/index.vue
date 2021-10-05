<template>
  
  <div class="text-center text-blue-400 mt-80 text-6xl">{{fetchedBalance}}</div>
  
</template>

<script>
import abi from "../Abi/abi";
import { ethers } from "ethers";

export default {
  components: {
    
  },
  data() {
    return {
      contractAddress: "your deployed contract address", // Contract Address.
      fetchedBalance: ""
      // balance: this.balance,
    };
  },
  async mounted() {
    this.totalbalance(), this.transfertoken()
  },

  methods: {
    async totalbalance() {
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      const myToken = new ethers.Contract(this.contractAddress, abi, provider);
      const balance = await myToken.balanceOf("your address goes here to chehk balanace ");
      this.fetchedBalance = balance;
      console.log(balance);
    },
    async transfertoken() {
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      await window.ethereum.enable();
      const signer = await provider.getSigner();
      //  console.log(await provider.getSigner().getAddress())
      const myToken = new ethers.Contract(this.contractAddress, abi, signer);
      const transfer = await myToken.transfer("address to whom you want to trasfer token","amount to transfer");
      console.log("transfer successful");
    },
    
  }
};
</script>
