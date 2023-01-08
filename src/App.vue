<script setup lang="ts">
const authURL = `https://www.bungie.net/en-us/OAuth/Authorize?client_id=26154&response_type=code`;
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

let code = getCode();
const openOAuth = ()=>{
  try{
    window.location.href = authURL;
  }catch(e){
    console.log(e);
  }
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
