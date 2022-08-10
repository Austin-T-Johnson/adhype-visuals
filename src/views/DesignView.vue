<template>
  
      <div class="h1-div">
        <h1 class="vision">YOUR VISION</h1>
        <br />
        <h1>From concept to completion, we got you.</h1>
      </div>

      <section class="scope-of-work-section">

        <div class="scope-of-work-container">
            <div v-for="(item,i) in designJson" :key="i" class="scope-of-work-item">
                <div class="scope-of-work-img">
                    <img :src="item.img" alt="">
                </div>
          <div class="scope-of-work-details">
          <div class="scope-of-work-title-container">
            <div class="scope-of-work-name">{{item.name}}</div>
            </div>
            <div class="scope-of-work-desc">{{item.desc}}</div>
          </div>
          </div>
        </div>

      </section>
 
</template>

<script>
import { defineComponent } from "vue";
import designJson from "../JSON/design.json"
export default defineComponent({
  name: "DesignView",
  data() {
    return {
        designJson
    };
  },
  methods: {},
  components: {},
});
</script>

<style scoped lang="scss">


h1,
h2,
h3,
h4,
h5 {
  color: white;
}

h2 {
  font-size: 2.5rem;
}

.vision {
  font-size: 3rem;
  font-family: $font;
  padding-top: 2%;
}

.scope-of-work-container{
 height:100%;
  max-width:3500px;
//   margin:auto;
  display:flex;
  padding:1%;
  gap:1%;
  flex-direction:row;
  align-items:stretch;
}
.scope-of-work-item{
  flex:1;
 border-radius:10px;
  overflow:hidden;
}
.scope-of-work-img{
  width:100%;
  height:400px;
  position: relative;
}
.scope-of-work-img img{
  width:100%;
  height:100%;
  object-fit:cover;
}
.scope-of-work-details{
  width:100%;
  padding:15px;
  color:white;
}

.scope-of-work-name{
  font-weight:bold;
  font-size:15pt;
}
.scope-of-work-position{
  font-weight:bold;
  font-size:15pt;
}
.scope-of-work-desc{
  margin-top:14px;
  font-size:12pt;
}

@media (max-width: 1024px) {
    .h1-div{
        padding-top:15%;
    }
    .scope-of-work-container{
        display:block;
        padding:28%;
       
    }
}

@media (max-width: 800px) {
    .scope-of-work-container{
        display:block;
        padding:20%;
        width:100%;
       
    }
}

@media (max-width: 480px) {
.scope-of-work-container{
        display:block;
        padding:7%;
        width:100%;
       
    }
}
</style>