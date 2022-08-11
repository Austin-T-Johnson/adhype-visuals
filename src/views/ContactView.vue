<template>
  <div class="contact-h1">
    <h1 class="contact-us">Contact Us</h1>
  </div>
  <section class="form">
    <div class="h2-div">
      <h2>Get in Touch</h2>
    </div>

    <form class="contact-form">
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
      <button @click="submit" type="submit">Send It!</button>
    </div>
  </section>
</template>

<script>
import { defineComponent } from "vue";
import axios from "axios";
import { reactive } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, minLength, email, alpha } from "@vuelidate/validators";

export default defineComponent({
  name: "ContactView",

  setup() {
    const state = reactive({
      name: "",
      email: "",
      message: "",
    });
    const rules = {
      name: { required },
      email: { required, email },
      message: { required },
    };

    const v$ = useVuelidate(rules, state, { $lazy: true });

    return { state, v$ };
  },

  data() {
    return {
      name: "",
      email: "",
      message: "",
    };
  },
  validations() {
    return {
      name: { required, alpha, minLength: minLength(1) },
      email: { required, email, minLength: minLength(1) },
      message: { required, minLength: minLength(1) },
    };
  },
  computed: {},
  methods: {
    async submit(e) {
      e.preventDefault();
      let post = { name: this.name, email: this.email, message: this.message };
      const isFormCorrect = await this.v$.$validate();
      try {
        if (!this.name && !this.email && !this.message) {
          this.$toast.error(`Please fill out all fields`, { position: "top" });
        } else if (!isFormCorrect) {
          await axios.post("/api/contact", post);
          this.$toast.success(`Message Sent!`, { position: "top" });
        }
      } catch (error) {
        console.log(error);
      } finally {
        (this.name = ""), (this.email = ""), (this.message = "");
      }
    },
  },
  components: {},
});
</script>

<style scoped lang="scss">
.contact-us {
  font-family: $font;
  color: white;
  font-size: 2.5rem;
  margin-top: 5%;
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

// .errorMessage {
//     color: red;
// }
// .hidden {
//     display: none;
// }

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
// .disabled {
//   margin-top: 20px;
//   font-size: 18px;
//   color: $light-grey-8;
//   font-weight: 800;
//   position: relative;
//   border: none;
//   background: none;
//   text-transform: uppercase;
// //   transition-timing-function: cubic-bezier(0.25, 0.8, 0.25, 1);
// //   transition-duration: 400ms;
// //   transition-property: color;
// }
// .disabled:hover {
//     color: $light-grey-8;
//     pointer-events: none;
// }

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

@media (max-width: 1024px) {
  .contact-h1 {
    padding-top: 15%;
  }
  .contact-form {
    width: 100%;
  }
}

@media (max-width: 800px) {
  .contact-form {
    width: 100%;
  }
}

@media (max-width: 480px) {
  .contact-h1 {
    padding-top: 25%;
  }
  .contact-form {
    width: 100%;
  }
}
</style>
