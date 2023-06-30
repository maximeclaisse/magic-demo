<template>
  <div>
    <span>{{ magicStatus }}</span>
    <span> - </span>
    <span v-if="loadingTime">{{ loadingTime }}ms</span>
  </div>
</template>

<script setup>
import { Magic } from "magic-sdk";

const magicStatus = ref("loading");
const loadingTime = ref(null);

onMounted(() => {
  let start = new Date();

  const magic = new Magic("pk_live_9824B74E7159DA7E", {
    network: {
      rpcUrl: "https://rpc-mumbai.maticvigil.com/",
      chainId: 80001,
    },
  });

  magic.user.isLoggedIn().on("settled", () => {
    let end = new Date();
    loadingTime.value = end.getTime() - start.getTime();
    magicStatus.value = "ready";

    console.log("settled");
  });
});
</script>

<style></style>
