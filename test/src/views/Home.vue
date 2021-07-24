<template>
  <div>
    <h1>Welcome to {{title2}}!</h1>
    <input type="text" v-model="input1" />
    <button type="button" @click="getData">Get</button>
    <button type="button" @click="setData">Set</button>
  </div>
</template>

<script>
  export default {
    name: "home",
    data() {
      return {
        title: "selectjun",
        title2: "Seoul",
        input1: "abcd"
      }
    },
    methods: {
      getData() {
        alert(this.input1)
      },
      setData() {
        this.input1 =  "123"
      }
    },
    beforeCreate() {
      console.log("beforeCreate")
    },
    created() {
      console.log("created")
    },
    beforeMount() {
      console.log("beforeMount")
    },
    mounted() {
      console.log("mounted")
    },
    beforeUpdate() {
      console.log("beforeUpdate")
    },
    updated() {
      console.log("updated")
    },
    beforeDestory() {
      console.log("beforeDestory")
    },
    destoryed() {
      console.log("destory")
    }
  }
</script>