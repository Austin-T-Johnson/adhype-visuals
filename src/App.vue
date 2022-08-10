<template>
<Header />
<Burger />
<router-view v-slot="{ Component, route }">
<transition name="fade">
    <div :key="route.name">
 <component :is="Component" />
 </div>
</transition>
</router-view>
</template>
<script>
import Header from './components/Header.vue'
import Burger from './components/Burger.vue'

export default {
    components:{
        Header,
       Burger
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

.fade-enter-from,
.fade-leave-to {
    opacity:0;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s ease-out;
}

</style>
