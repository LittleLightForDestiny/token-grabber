<script setup lang="ts">
const authURL = `https://www.bungie.net/en-us/OAuth/Authorize?client_id=26263&response_type=code`;
const getCode = () => {
  const search = window.location.search;
  const args = search.split(/[?&]/).filter((a)=>!!a).map((v)=>v.split('=')).map((v)=>({key:v[0], value:v[1]}));
  for(let arg of args){
    if(arg.key == 'code'){
      return arg.value;
    }
  }
  return null;
}

const code = getCode();
const openOAuth = ()=>{
  window.location.href = authURL;
};
</script>

<template>
  <header>
  </header>

  <main>
    <button v-if="!code" @click="openOAuth()">Login with Bungie</button>
    <div v-else>
      Your code is {{ code }}
    </div>
  </main>
</template>

<style scoped>
</style>
