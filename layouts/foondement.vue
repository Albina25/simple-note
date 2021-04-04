<template>
  <div class="foondament">
  <header class="foondament-header">
  <nuxt-link to="/" class="header-link-main">записная книга</nuxt-link>
  
  <button class="header-link" @click="openModal">создать</button>
  <button class="header-link" @click="openModal">завершить</button>
  <button class="header-link" @click="openModal">Взять в работу</button>
  <button class="header-link" @click="openModal">удалить</button>
   
  </header>
    <Nuxt />
  </div>
</template>

<script>
export default {
  data: () => ({
  
  
  }),
  methods: {
    openModal() {
    this.$nuxt.$emit('showDialog')
   }
  
}
}
</script>
<style lang="scss">
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.foondament-header {
display: flex;
align-items: center;
}

.header-link {
   padding: 0.1rem;
   height:1.5rem;
   margin-right: 1rem;
   text-transform: uppercase;
   font-family: 'Montserrat', sans-serif;
   text-decoration: none;
   border-radius: 25px;
   
}
   .header-link-main {
       font-weight: bold;
       padding: 1rem;
       margin-right: 1rem;
       text-transform: uppercase;
       text-decoration: none;
       font-size: 25px;
   }


.header-link:last-of-type {
 margin-right: 0;
}

html, body, #__nuxt, #__layout, .foondament {
height: 100%;
width: 100%;}

html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 18px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}
</style>
