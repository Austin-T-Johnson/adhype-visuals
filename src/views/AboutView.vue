<template>
  <div class="background">
    <div class="about-div">
      <h1 class="about-txt">About Us</h1>
      <h3>
        Adhype Visuals is in its second year as a creative content studio specializing in visual experiences. We are a team of designers, web developers, video engineers, and programmers that focus on live events, web design, graphic design, and virtual streaming showcases. We create visually stunning experiences uniquely designed for individual artists or the event as a whole. Our background in the touring music industry and the corporate world has taught us to focus on the visual story that provides memorable moments to the audiences.
      </h3>
    </div>

    <section class="team-section">
      <div class="team-container">
        <div v-for="(item, i) in teamMembers" :key="i" class="team-item">
          <div class="team-img">
            <img :src="item.img" alt="" />
          </div>
          <div class="team-details">
            <div class="team-title-container">
              <div class="team-name">{{ item.name }}</div>
              <div class="team-position">{{ item.position }}</div>
            </div>
            <div class="team-desc">{{ item.desc }}</div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>



<script>
import { defineComponent } from "vue";
import teamMembers from "../JSON/team.json";
export default defineComponent({
  name: "AboutView",
  data() {
    return {
      image: "@../assets/images/abstract-lines.jpeg",
      teamMembers,
    };
  },
  methods: {},
  components: {},
});
</script>

<style scoped lang="scss">
.background {
  height: 100%;
  width: 100%;
}

.aht {
  width: 100%;
}
.about-div {
  z-index: 2;
  top: 0;
  left: 0;
  position: relative;
  width: 50%;
  margin: 0 auto;
}

.about-txt {
  font-family: $font;
  font-size: 2.5rem;
}
h1 {
  color: white;
  padding-top: 5%;
}

h2,
h3,
h4 {
  color: white;
}

.team {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  z-index: 2;
  width: 100%;
  height: 100%;
}

.txt {
  position: relative;
  width: 40vh;
  height: 39vh;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.6);
  color: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 4rem;
  opacity: 0;
  transition: opacity 0.25s;
  font-size: 2.5rem;
}
.txt:hover {
  opacity: 1;
}

.team-container {
  height: 100%;
  max-width: 1500px;
  margin: auto;
  display: flex;
  padding: 15px;
  gap: 100px;
  flex-direction: row;
  align-items: stretch;
}
.team-item {
  flex: 1;
  border-radius: 10px;
  overflow: hidden;
}
.team-img {
  width: 100%;
  height: 400px;
  position: relative;
}
.team-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.team-details {
  width: 100%;
  padding: 15px;
  color: white;
}

.team-name {
  font-weight: bold;
  font-size: 15pt;
}
.team-position {
  font-weight: bold;
  font-size: 15pt;
}
.team-desc {
  margin-top: 14px;
  font-size: 12pt;
}

@media (max-width: 1024px) {
}

@media (max-width: 800px) {
  .about-div {
    width: 100%;
    padding: 10%;
  }
  .team-container {
    display: block;
    padding: 5% 25%;
  }
}

@media (max-width: 480px) {
  .about-div {
    width: 100%;
    padding: 10%;
  }
  .team-container {
    display: block;
  }
}
</style>

