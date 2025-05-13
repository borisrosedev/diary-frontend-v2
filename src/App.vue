<template>
  <main>
    <form @submit.prevent="submitHandler">
      <div class="field">
        <p class="control has-icons-left has-icons-right">
          <input 
            class="input" 
            type="email" 
            placeholder="Email"
            v-model="data.email" 
          />
          <span class="icon is-small is-left">
            <i class="fas fa-envelope"></i>
          </span>
          <span class="icon is-small is-right">
            <i class="fas fa-check"></i>
          </span>
        </p>
      </div>
      <div class="field">
        <p class="control has-icons-left">
          <input 
            class="input" 
            type="password" 
            placeholder="Password"
            v-model="data.password" 
          />
          <span class="icon is-small is-left">
            <i class="fas fa-lock"></i>
          </span>
        </p>
      </div>
      <div class="field">
        <p class="control">
          <button type="submit" class="button is-success">Login</button>
        </p>
      </div>
    </form>
  </main>
</template>
<script lang="ts" setup>
import { reactive } from "vue"


const data = reactive({})


async function submitHandler () {

  const url = 'http://localhost:3000/api/v1/user/login'
  const req = {
    method: "POST",
    headers : {
      "Content-Type":"application/json"
    },
    body: JSON.stringify({ email: data.email, password: data.password })
  }

  try {
    const { token } = await (await fetch(url,req)).json()

    localstorage.setItem('token', token)
    
  } catch(err) {
    console.log(err)
  }

}

</script>

<style lang="scss">
main {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
