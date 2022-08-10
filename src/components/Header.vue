<template>
  <div class="header">
 
    <router-link v-if="this.$route.path === '/'" style="color: white" class="nav" to="/"><li>Home</li></router-link>
    <router-link v-else class="nav" to="/"><li>Home</li></router-link>

    <router-link v-if="this.$route.path === '/about'" style="color: white" class="nav" to="/about"><li>About</li></router-link>
    <router-link v-else class="nav" to="/about"><li>About</li></router-link>

    <router-link v-if="this.$route.path === '/design'" style="color: white" class="nav" to="/design"><li>Design</li></router-link>
    <router-link v-else class="nav" to="/design"><li>Design</li></router-link>

   <router-link v-if="this.$route.path === '/contact'" style="color: white" class="nav" to="/contact"><li>Contact</li></router-link>
  <router-link v-else class="nav" to="/contact"><li>Contact</li></router-link>

 
  </div>

</template>
<script>
export default {
  name: "mainHeader",
  data() {
    return {};
  },
  mounted() {},
  methods: {},
  computed: {},
};
</script>
<style scoped lang="scss">
.header{
    width:100%;
    position: absolute;
    top:0;
    padding-right: 2%;
    z-index: 3;
    display: flex;
    justify-content: right;
    gap: 15px;
    align-items: center;
   

.nav {
   text-decoration: none;
    color:darkgray;
    list-style:none
}
}

@media (max-width: 728px) {
    .header{
    display:none
 
}
}





</style>