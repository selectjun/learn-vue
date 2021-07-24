<template>
  <div>
    <h1>Welcome to {{title2}}!</h1>
    <input type="text" v-model="input1" />
    <button type="button" @click="getData">Get</button>
    <button type="button" @click="setData">Set</button>

    <select class="form-control" v-model="region" @change="changeRegion">
      <option :key="index" :value="data.v" v-for="(data, index) in options">{{data.t}}</option>
    </select>

    <table class="table table-bordered" v-if="tableShow">
      <tr :key="index" v-for="(data, index) in options">
        <td>{{data.v}}</td>
        <td>{{data.t}}</td>
      </tr>
    </table>

    <table class="table table-bordered" v-show="tableShow">
      <tr :key="index" v-for="(data, index) in options">
        <td>{{data.v}}</td>
        <td>{{data.t}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
  export default {
    name: "home",
    data() {
      return {
        title: "selectjun",
        title2: "Seoul",
        input1: "abcd",
        options: [
          { v: "S", t: "Seoutl" },
          { v: "J", t: "Jenu" },
          { v: "B", t: "Busan" }
        ],
        region: "J",
        tableShow: true
      }
    },
    watch: {
      input1() {
        console.log(this.input1);
      }
    },
    methods: {
      getData() {
        alert(this.input1)
      },
      setData() {
        this.input1 =  "123"
      },
      changeRegion() {
        alert(this.region)
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