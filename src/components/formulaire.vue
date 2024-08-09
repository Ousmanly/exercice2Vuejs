<template>
  <section>
    <h1>Formulaire</h1>
    <form @submit.prevent="validation">
    <div>
        <label for="nom">Name</label>
        <input id="nom" type="text" v-model="name" @blur="valideName">
        <span v-if="errors.name" class="error">{{ errors.name}}</span>
    </div>
    <div>
        <label for="email">Email</label>
        <input id="email" type="email" v-model="email" @blur="valideEmail">
        <span v-if="errors.email" class="error">{{ errors.email }}</span>
    </div>
    <div>
        <label for="phone">Phone</label>
        <input id="phone" type="tel" v-model="phone" @blur="validePhone">
        <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
    </div>
    <button>Envoye</button>
  </form>
  <p v-if="message" class="message" >{{ message }}</p>
  </section>
</template>

<script setup>
import { ref } from "vue";

const name = ref('');
const email = ref('');
const phone = ref('');
const errors = ref({});
const message = ref('');


function valideName() {
    const namePattern = /^[^0-9]+$/;
    errors.value.name = namePattern.test(name.value) ? '' : 'Le nom est invalide.';
}
const valideEmail = () => {
  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  errors.value.email = emailPattern.test(email.value) ? '' : 'Email invalide.';
};

const validePhone = () => {
  const phonePattern = /^\+?[0-9\s\-]{7,15}$/;
  errors.value.phone = phonePattern.test(phone.value) ? '' : 'Numéro de téléphone invalide.';
};

function validation() {
    valideName()
    valideEmail()
    validePhone()

    if (!errors.value.name && !errors.value.email && !errors.value.phone) {
        message.value = 'Formulaire soumis avec succès!';
        name.value = '';
        email.value = '';
        phone.value = '';
    } else {
        message.value = '';
    }
}
</script>

<style scoped>
h1{
    text-align: center;
    font-size: 35px;
}
section{
    width: 400px;
    margin: auto;
    padding: 20px;
    border: 2px solid green;
    border-radius: 10px;
    background-image: url("src/graphic-tablet.jpg");
}
input{
    height: 30px;
    margin-bottom: 10px;
    border-radius: 5px;
}
button{
    width: 400px;
    height: 35px;
    background-color: green;
    color: white;
    border: none;
    border-radius: 10px;
    font-weight: bold;
    cursor: pointer;
}
button:active{
    transform: scale(1.03);
    background-color: rgb(8, 93, 8);
}
div{
    display: flex;
    flex-direction: column;
}
.error{
    color: red;
}
.message{
    color: green;
}
</style>
