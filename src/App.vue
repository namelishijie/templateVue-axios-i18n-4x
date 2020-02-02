<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view v-if="isAlive"/>
    {{ $t('home.title') }}
    <button @click="onLang">切换语言</button>


    <input v-model="value" type="text" v-validate="'required|email'" name="email" data-vv-scope="login" data-vv-validate-on="blur">
    <p v-show="errors.has('login.email')">{{ errors.first('login.email') }}</p> 
    <button @click="onDemo">确定</button>


  </div>
</template>

<script>
export default {
  name: 'App',
  provide() {
    return {
      reload: this.reload
    }
  },
  data() {
    return {
      isAlive: true
    }
  },
  methods: {
    reload() {
      this.isAlive = false
      this.$nextTick(function () {
        this.isAlive = true
      })
    },
    onLang() {
      this.$lang(this.$store.getters.lang == 'en' ? 'zh_cn' : 'en')
    },
    onDemo() {
      this.$validator.validateAll('login').then(res => {
        console.log(res)
      })
    }
  },
  created() {
    // this.$http.index()
    // .then(res =>{
    //   console.log(res)
    // })
  }
}
</script>

<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
