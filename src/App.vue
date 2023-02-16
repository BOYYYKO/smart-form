<script>

import MyModal from './components/MyModal.vue'
import StarRating from './components/StarRating.vue'
import Teleport from 'vue2-teleport'

export default {
  components: {
    MyModal,
    StarRating,
    Teleport
  },

  data() {
    return {
      username: "",
      email: "",
      message: "",
      show: false,
      show2: false,
      showModal: false,
      showModal2: false,
    }
  },
  
  methods: {
    isFilled() {
      if (!this.username || !this.email || !this.message) {
        this.show2 = false
      } else {
        this.show2 = true
      }
    },

    isCorrectEmail(email) {
      if (/^[A-z-/.][\w-]+@([\w-]+\.)+[\w-]{2,4}$/.test(email) == false)
        this.show = true
      else
        this.show = false
    },

    submit() {
      const form = document.getElementById("form");
      form.addEventListener("submit", (e) => {
        e.preventDefault();
        const inputs = document.querySelectorAll("input, textarea");

        const objectForm = Array.from(inputs).reduce((obj, field) => {
          obj[field.name] = field.value;
          return obj;
        }, {});

        console.log(JSON.stringify(objectForm));
      });
      const code = Math.floor(Math.random() * 200);
        if(code == 200){
          this.showModal2 = true
        } else {
          this.showModal = true
        }
    }
  }
}
</script>

<template>
  <div id="app">
    <form id="form" class="form" @input="isFilled()">
      <h2>FEEDBACK FORM</h2>
      <input v-model="username" type="text" name="username" placeholder="Name">
      <label v-if="show" for="email">Please paste correct email</label>
      <input v-model="email" type="email" name="email" placeholder="Email" @input="isCorrectEmail($event.target.value)">

     <div> <StarRating :rating="0"/></div>

      <textarea v-model="message" name="message" id="message" placeholder="Comment" cols="30" rows="10"></textarea>
      <button v-if="show2" @click="submit()" class="button" type="submit">Send feedback</button>
    </form>

    <Teleport to="body">
      <my-modal :show="showModal" @close="showModal = false">
        <template #header>
          <h3>Something went wrong.</h3>
        </template>
      </my-modal>
    </Teleport>

    <Teleport to="body">
      <my-modal :show="showModal2" @close="showModal2 = false">
        <template #header>
          <h3>Thank you!</h3>
        </template>
      </my-modal>
    </Teleport>
  </div>
</template>

<style>
.form {
  background-color: #f8f8f8;
  display: grid;
  justify-content: center;
  margin: auto;
  width: 50%;
  padding: 15px 0px;
  border: 5px #ccc solid;
  width: 65%;
  justify-items: center;
}

h2 {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h3 {
  display: flex;
  justify-content: center;
}


input {
  width: 100%;
  padding: 12px 20px;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: white;
  resize: none;
  margin: 10px 0px;
}

textarea {
  width: 100%;
  height: 150px;
  margin: 10px 0px;
  padding: 12px 20px;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: white;
  resize: none;
}

.button {
  background-color: #6633FF;
  border: none;
  color: white;
  margin: 10px 10px;
  padding: 8px 64px;
  border-radius: 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>