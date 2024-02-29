<script setup lang="ts">
const emailInput = ref("");
const card = ref(true);
const cardSuccess = ref(false);
let toggleIsValidateEmail = () => {
  card.value = true;
  emailInput.value = "";
  cardSuccess.value = false;
  toggleValidateEmail.value = false;
};

let toggleValidateEmail = ref(false);

function validateEmail() {
  const email = emailInput.value;
  const emailRegex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
  if (!emailRegex.test(email)) {
    toggleValidateEmail.value = true;
  } else {
    cardSuccess.value = true;
    card.value = false;
    console.log("email :", email);
  }
}
</script>

<template>
  <div></div>
  <div class="w-full h-auto">
    <div v-if="card" class="flex justify-center">
      <div
        class="card-signIn container bg-white rounded-3xl sm:m-0 lg:m-[20%] grid lg:grid-cols-2"
      >
        <div
          class="left text-[#242742] flex justify-center flex-col sm:m-6 lg:m-10"
        >
          <h1 class="sm:text-4xl lg:text-5xl font-bold">Stay updated!</h1>
          <p class="my-3">
            Join 60,000+ product managers receiving monthly <br />
            updates on:
          </p>
          <div>
            <ul class="">
              <div class="flex flex-row justify-start items-center">
                <img
                  src="../assets/images/icon-list.svg"
                  class="sm:pr-2 lg:pr-3"
                  alt="icon-list"
                />
                <li class="my-2">
                  Product discovery and building what matters
                </li>
              </div>
              <div class="flex flex-row justify-start items-center">
                <img
                  src="../assets/images/icon-list.svg"
                  class="sm:pr-2 lg:pr-3"
                  alt="con-list"
                />
                <li class="my-2">Measuring to ensure updates are a success</li>
              </div>
              <div class="flex flex-row justify-start items-center">
                <img
                  src="../assets/images/icon-list.svg"
                  class="sm:pr-2 lg:pr-3"
                  alt="con-list"
                />
                <li class="my-2">And much more!</li>
              </div>
            </ul>
          </div>
          <div class="flex flex-col">
            <label
              for="email"
              class="text-[#242742] font-semibold text-xs mt-3 mb-1"
            >
              Email address
            </label>
            <div
              v-if="toggleValidateEmail"
              class="text-red-500 text-xs font-semibold flex justify-end"
            >
              Valid email required
            </div>
            <input
              @keydown.enter="validateEmail"
              v-model.trim="emailInput"
              placeholder="email@company.com"
              type="email"
              class="h-[3em] cursor-pointer border-[1px] border-gray-400 rounded-md p-2 mb-3 w-full"
              :class="{
                'border-red-500 text-red-500 active:border-red-500 bg-red-500 bg-opacity-10 ':
                  toggleValidateEmail,
              }"
            />
            <button
              @click="validateEmail"
              class="text-white cursor-pointer bg-[#242742] hover:bg-[#ff6257] active:bg-[#ff6257] my-3 rounded-md font-medium w-[100%] h-[3em]"
            >
              Subscribe to monthly newsletter
            </button>
          </div>
        </div>
        <div class="right">
          <div class="pic sm:hidden m-4 aspect-square overflow-hidden">
            <img
              src="../assets/images/illustration-sign-up-desktop.svg"
              class="sign-up-desktop w-ful sign-up-pic h-auto object-cover"
              alt="sign-up-desktop"
            />
          </div>
          <div class="">
            <img
              class="sign-up-mobile w-full sign-up-pic h-auto object-cover"
              src="../assets/images/illustration-sign-up-mobile.svg"
              alt="sign-up-"
            />
          </div>
        </div>
      </div>
    </div>

    <!-- Modal success -->
    <div v-if="cardSuccess" class="flex justify-center cardSuccess">
      <div class="bg-white success-cont lg:p-10 lg:rounded-2xl z-40">
        <img
          src="../assets/images/icon-success.svg"
          class="my-2 sm:my-4 w-16"
          alt="icon-success"
        />
        <h1 class="text-3xl font-semibold">Thanks for subscribing!</h1>

        <p>
          A confirmation email has been sent to <br />
          <span class="font-semibold">{{ emailInput }}</span
          >. Please open it and click <br />
          the button to confirm your subscription. <br />
        </p>
        <div class="divBut">
          <button
            @click="toggleIsValidateEmail"
            class="text-white cursor-pointer success-but lg:bg-[#ff6257] my-3 rounded-md font-medium w-full h-10"
          >
            Dismiss message
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@media screen and (max-width: 375px) {
  .container {
    width: 100%;
    display: flex;
    flex-direction: column-reverse;
    justify-content: center;
    margin: 0;
    border-radius: 0;
  }
  .sign-up-desktop {
    display: none;
  }

  h1 {
    font-size: 2.25em;
  }
  .success-cont {
    padding: 3em;
    border-radius: 0;
    display: flex;
    flex-direction: column;
    padding-top: 10em;
    /* justify-content: center; */
    gap: 1em;
  }
  .success-but {
    background-color: #242742;
    margin-top: 12em;
  }
  .cardSuccess {
    position: absolute;
    top: 0%;
    left: 0%;
    width: 100%;
    height: 100%;
  }
}

@media screen and (min-width: 376px) {
  .sign-up-mobile {
    display: none;
  }
  .cardSuccess {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}
</style>
