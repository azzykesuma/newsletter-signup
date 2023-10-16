<template>
  <main>
    <div v-if="!subscribed" class="mainContainer">
      <div class="top">
        <picture>
          <source srcset="./assets/images/illustration-sign-up-mobile.svg" media="(max-width: 768px)" />
          <source srcset="./assets/images/illustration-sign-up-desktop.svg" media="(min-width: 769px)" />
          <img src="./assets/images/illustration-sign-up-desktop.svg" alt="hero image" />
        </picture>
      </div>
      <div class="bottom">
        <h1>Stay updated!</h1>
        <p class="subHeader_text">Join 60,000+ product managers receiving monthly updates on:</p>
        <ul>
          <li>
            <div class="listContainer">
              <div class="icon"><img src="./assets/images/icon-list.svg" /></div>
              <p class="content">Product discovery and building what matters</p>
            </div>
          </li>
          <li>
            <div class="listContainer">
              <div class="icon"><img src="./assets/images/icon-list.svg" /></div>
              <p class="content">Measuring to ensure updates are a success</p>
            </div>
          </li>
          <li>
            <div class="listContainer">
              <div class="icon"><img src="./assets/images/icon-list.svg" /></div>
              <p class="content">And much more!</p>
            </div>
          </li>
        </ul>
        <form action="#">
          <div class="formContainer">            
            <label for="email">Email address</label>
            <!-- giving the type of text to give custom error handling -->
            <input type="text" name="email" :value="email" placeholder="email@company.com"/>
            <button type="submit" @click="submit">Subscribe to monthly newsletter</button>
            <p id="error" class="errorText"></p>
          </div>
        </form>
      </div>
    </div>
    <div v-else>
      <div class="successContainer">
        <img src="./assets/images/icon-success.svg"  alt="success-icon"/>
        <h1>Thanks for subscribing!</h1>
        <p>
          A confirmation email has been sent to <strong style="color:hsl(234, 29%, 20%)">{{ emailVal }}</strong>. 
          Please open it and click the button inside to confirm your subscription.
        </p>
        <button @click="returnToNewsletter" class="dismissBtn">Dismiss message</button>
      </div>
    </div>
  </main>
</template>
<script setup>
import { ref } from 'vue';
let emailVal = ref('');
let subscribed = ref(false);
const submit = (e) => {
  e.preventDefault();
  const email = document.querySelector('input[name="email"]').value;
  const error = document.getElementById('error');
  const pattern = /^[^ ]+@[^ ]+\.[a-z]{2,3}$/;
  if (email.match(pattern)) {
    error.style.display = 'none';
    if (localStorage.getItem('email') === email) {
      error.style.display = 'block';
      error.textContent = 'Email already subscribed';
    } else {
      subscribed.value = true;
      emailVal.value = email;
    }
  } else if (email === '') {
    error.style.display = 'block';
    error.textContent = 'Email cannot be blank';
  } else {
    error.style.display = 'block';
    error.textContent = 'Valid email required';
  }
};
const returnToNewsletter = () => {
  subscribed.value = false;
  localStorage.setItem('email', emailVal.value);
};

</script>