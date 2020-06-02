<template>
  <div class="login">
    <div class="title"><span>Member Login</span></div>
    <div class="form-container">
      <div class="form-control">
        <txtBox :iconClass="'fa-user'" :showIcon="true"  @input="(val)=>username = val" :placeholder="'Username'" />
      </div>
      <div class="form-control">
        <txtBox :iconClass="'fa-lock'" :showIcon="true" @input="(val)=>password = val" type="password" :placeholder="'Password'" />
      </div>
      <div class="form-control links">
        <chkBox :label="'Remember Me'" @change="handleChange" />
        <span class="wrap" @click="handleClick"><i>Forgot Password?</i></span>
      </div>
      <div class="form-control last">
        <button @click="handleLogin">Login</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import '@/assets/css/font-awesome.min.css'

export default {
  components: {
    txtBox: () => import('@/components/textBoxComponent.vue'),
    chkBox: () => import('@/components/checkBoxComponent.vue')
  },
  data () {
    return {
      username: '',
      password: '',
      rememberMe: false
    }
  },
  created () {
    document.title = 'Login'
  },
  methods: {
    handleLogin () {
      if (this.username && this.password) {
        const isValid = this.username.match(/^[a-z]+@[a-z]+?\.[a-z]{3}$/)
        if (isValid) {
          this.login()
        } else {
          alert('Wrong email')
        }
      } else {
        alert('Enter data')
      }
    },
    async login () {
      try {
        const { data } = await axios.post('http://www.mocky.io/v2/5ed661f03400006f0006d9f3', {
          username: this.username,
          password: this.password
        })
        alert(`Login done. Token is ${data.authToken}`)
      } catch (error) {
        const msg = error.response ? error.response.data.message : error.message
        console.error('Error in login', msg)
      }
    },
    handleChange (val) {
      this.rememberMe = val
    },
    /* handleInput (val) {
      if (val) this.username = val.trim()
    },
    handleInput2 (val) {
      if (val) this.password = val.trim()
    }, */
    handleClick () {
      alert('So sad, too bad.')
    }
  }
}
</script>
<style scoped>
.form-container{
  width: 100%;
  display: flex;
  flex-direction: column;
}
button{
  background: orange;
  color: white;
  border: 1px solid;
  border-radius: 8px;
  margin: 0px 5px;
  padding: 10px 50px;
}

.form-control{
  margin: 0 auto;
  padding: 8px;
  width: 270px;
}
.form-control >>> .checkbox{
  color: rgba(0,0,0,0.4);
  font-size: 12px;
  padding: 5px;
  /* display: inline-block; */
  float: left;
}
.form-control >>> .checkbox input{
  vertical-align: bottom;
}
.form-control >>> .checkbox input:checked{
  vertical-align: bottom;
  filter: grayscale(1)
}
.form-control >>> ::placeholder {
  color: rgba(0,0,0,0.4);
  opacity: 1;
}
.links{
  padding: 4px;
  display: flex;
  justify-content: space-between;
}
.wrap{
  padding: 5px;
  display: inline-block;
}
.last{
  text-align: left;
}
i{
  padding: 2px;
  font-size: 12px;
  color: rgba(0,0,0,0.4);
  float: right;
  cursor: pointer;
}
</style>
