<template>
  <transition enter-active-class="fadeIn" leave-active-class="fadeOut">
    <div v-if="modal" @click="modal = false" class="modal animated">
      <img :src="activeModalSrc" alt="" />
    </div>
  </transition>
  <div class="top-background-img"></div>

  <div class="adhype-container">
    <h1>Adhype Visuals</h1>
    <h2 class="description">
      Your one-stop shop for <br /><br />Visual Content, Web Design, Creative
      Direction, Graphic Design & Branding
    </h2>
  </div>

  <div class="worked-with">
    <h1 class="worked-with">Artists we have worked with</h1>
  </div>

  <!-- Artists -->

  <section class="bottom-container">
    <div
      @click="(activeModalSrc = item.img), (modal = true)"
      v-for="(item, i) in artists"
      :key="i"
      class="artist-imgs-container"
    >
      <div class="artist-img-div">
        <img :src="item.img" alt="Artist Pics" />
      </div>

      <div class="txt-container">
        <div class="artist-txt">{{ item.txt }}</div>
      </div>
    </div>
  </section>

  <!-- Contact -->

  <section class="form">
    <div class="h2-div">
      <!-- {{msg}} -->
      <h2 class="get-in-touch">Get in Touch</h2>
    </div>

    <form @submit="submit" class="contact-form" method="POST" action="contact">
      <div class="input-div">
        <label class="label">Name</label>
        <input v-model="name" class="input-input" type="text" />
      </div>

      <div class="input-div">
        <label class="label">Email</label>
        <input v-model="email" class="input-input" type="text" />
      </div>

      <div class="input-div">
        <label class="label">Message</label>
        <input v-model="message" class="input-input" type="text" />
      </div>
    </form>
    <div class="btn-content">
      <button @click="submit">Send It!</button>
    </div>
  </section>
</template>

<script>
import { defineComponent } from "vue";
import artists from "../JSON/artists.json";
import axios from "axios";
export default defineComponent({
  name: "HomeView",

  data() {
    return {
      name: "",
      email: "",
      message: "",
      modal: false,
      artists,
    };
  },
  computed: {},
  methods: {
    async submit(e) {
      e.preventDefault();
      let post = { name: this.name, email: this.email, message: this.message };
      try {
        if (this.name == "" || this.email == "" || this.message == "") {
          this.$toast.error(`Please fill out all fields`, { position: "top" });
        } else {
          await axios.post("/api/contact", post);
          this.$toast.success(`Message Sent!`, { position: "top" });
          (this.name = ""), (this.email = ""), (this.message = "");
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
  components: {},
});
</script>

<style scoped lang="scss">
.modal {
  position: fixed;
  height: 100vh;
  width: 100vw;
  top: 0;
  left: 0;
  z-index: 10;
  img {
    height: 100%;
    width: 100%;
    object-fit: cover;
  }
}

h1 {
  font-family: $font;
  font-size: 4rem;
  color: white;
}

.top-background-img {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  background-image: url("../assets/images/fever-shoot.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.adhype-container {
  position: absolute;
  z-index: 1;
  color: white;
  height: 100vh;
  width: 100%;
  background: RGB(0, 0, 0, 0.5);
  top: 0;
  display: flex;
  flex-wrap: wrap;
  align-items: center;

  h1 {
    width: 100%;
    color: $white;
  }

  h2 {
    width: 100%;
    margin-bottom: 25%;
    font-size: 2rem;
    color: $white;
  }
}

.worked-with {
  height: 1vh;
  width: 100%;
  margin: 5% 0;
  h1 {
    font-family: $font;
    font-size: 4rem;
    color: $white;
    height: 10vh;
    align-items: center;
  }
}
.bottom-container {
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: center;
}

.artist-imgs-container {
  display: flex;
  border-radius: 5%;
  overflow: hidden;
  align-items: center;
  justify-content: center;
  height: 40vh;
  width: 40vh;
  position: relative;
  flex-wrap: wrap;
}

.artist-img-div {
  position: relative;
  cursor: pointer;
  height: 100%;
  width: 100%;
  img {
    height: 100%;
    width: 100%;
    object-fit: cover;
  }
}

.artist-txt {
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
.artist-txt:hover {
  opacity: 1;
}

.txt-container {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 5px solid black;
  border-radius: 5%;
  cursor: pointer;
  overflow: hidden;
}

h2 {
  color: white;
  font-size: 2rem;
}

.form {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 50vh;
  width: 100%;
  margin: 0 auto;
}

.contact-form {
  width: 50%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.input-div {
  position: relative;
  padding: 20px 0 0;
  margin-top: 10px;
  width: 100%;
  max-width: 50%;
}

.input-input {
  width: 100%;
  border: none;
  border-bottom: 2px solid darkgray;
  outline: 0;
  font-size: 1rem;
  color: white;
  background: transparent;
  transition: border-color 0.2s;
  padding-top: 15px;
}

.input-input::placeholder {
  color: transparent;
}

.input-input::placeholder-shown ~ .input-input {
  font-size: 1.5rem;
  cursor: text;
  top: 20px;
}

.label {
  position: absolute;
  top: 0;
  display: block;
  transition: 0.2s;
  font-size: 1.5rem;
  color: white;
  pointer-events: none;
}

.label:focus {
  padding-bottom: 6px;
  font-weight: 700;
  border-width: 3px;
  border-image: linear-gradient(to right, #116399, #38caef);
  border-image-slice: 1;
}

.label:focus ~ .label {
  position: absolute;
  top: 0;
  display: block;
  transition: 0.2s;
  font-size: 17px;
  color: #38caef;
  font-weight: 700;
}

.label:required,
.label:invalid {
  box-shadow: none;
}

button {
  margin-top: 20px;
  font-size: 18px;
  color: white;
  font-weight: 800;
  cursor: pointer;
  position: relative;
  border: none;
  background: none;
  text-transform: uppercase;
  transition-timing-function: cubic-bezier(0.25, 0.8, 0.25, 1);
  transition-duration: 400ms;
  transition-property: color;
}

button:focus,
button:hover {
  color: #fff;
}

button:focus:after,
button:hover:after {
  width: 100%;
  left: 0%;
}

button:after {
  content: "";
  pointer-events: none;
  bottom: -2px;
  left: 50%;
  position: absolute;
  width: 0%;
  height: 2px;
  background-color: #fff;
  transition-timing-function: cubic-bezier(0.25, 0.8, 0.25, 1);
  transition-duration: 400ms;
  transition-property: width, left;
}

.animated {
  -webkit-animation-duration: 0.4s;
  animation-duration: 0.4s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

@media (max-height: 960px) {
  .artist-imgs-container {
    height: 40vh;
    width: 45vh;
    position: relative;
    flex-wrap: wrap;
  }
  .artist-txt {
    width: 45vh;
  }
}

@media (max-width: 1024px) {
  .worked-with {
    margin: 16% 0;
  }
  .bottom-container {
    height: 100%;
  }
  .contact-form {
    width: 100%;
  }
}
@media (max-width: 800px) {
  .worked-with {
    margin-bottom: 25%;
  }
  .contact-form {
    width: 100%;
  }
  .adhype-container {
    position: absolute;
    z-index: 1;
    color: white;
    height: 100vh;
    width: 100%;
    background: RGB(0, 0, 0, 0.5);
    top: 0;
    display: block;
    padding-top: 10%;
    align-items: center;
  }
}

@media (max-width: 480px) {
  .worked-with {
    margin-bottom: 66%;
  }
  .contact-form {
    width: 100%;
  }
}
</style>