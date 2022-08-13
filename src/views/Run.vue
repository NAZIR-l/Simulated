<template>
  <div class="containers">
    <div v-if="SHOWS">
      <div class="header">
        <h1>Category OverView</h1>
      </div>
      <hr style="background-color: red; height: 2px; width: 760px" />
      <br />
      <div class="header2">
        <h2>Unnamed Project</h2>
      </div>
      <div class="header3">
        <p>
          Replication : {{ Replication }} --------------------- Time Unit :
          Hours
        </p>
      </div>

      <div class="header4">
        <h2>Key Performance Indicarors</h2>
      </div>
      <div style="display: inline-flex; padding-top: 50px">
        <div style="padding-right: 550px;">
<h4 style="color:blue;">SYstem</h4>
        
        <p style="color: blue">Average</p>
        
        </div>
        <div >
        <h3 style="color: red">Number Out</h3>
        <p style="color: red">{{ maxCreate }}</p>
        </div>
        
          <h1>{{errorMessage}}</h1>

      </div>
    </div>

    <div v-else>
      <div class="header">
        <h1>User Specifited</h1>
      </div>
      <hr style="background-color: red; height: 2px; width: 760px" />
      <br />
      <div class="header2">
        <h2>Unnamed Project</h2>
      </div>
      <div v-for="key in Replication" :key="key">
        <div class="row align-items-start" style="padding-top: 50px">
          <div class="col">Replication : {{ key }}</div>
          <div class="col">Start time : 0.00</div>
          <div class="col">Stop time 5.00</div>
          <div class="col">Time Unit : Hours</div>
        </div>
        <div style="display: flex">
          <h3>Counter</h3>
          <hr style="background-color: red; height: 2px; width: 760px" />
        </div>
        <div style="display: flex">

          <h3 >{{ NameAssign }}  : {{arrayX[key]}}</h3>
          
        </div>
      </div>
    </div>

    <div v-if="SHOWS">
      <button class="btn btn-danger" @click="USERPPge">NEXT</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["Replication", "length", "maxCreate", "NameAssign","CONSTVALUE",'errorMessage','arrayX' ],
  data() {
    return {
      SHOWS: true,
      loop: 1,
    };
  },
  methods: {
    USERPPge() {
      this.SHOWS = !this.SHOWS;
    },
    Pluse() {
      this.loop = this.loop + 1;
      console.log("Loop: " + this.loop);
    },
  },
};
</script>

<style>
.header2 {
  position: absolute;
  border-top: 2px solid red;
}
.containers {
  padding: 13px;
  margin: 13px;
}
.header3 {
  padding: 50px;
  position: absolute;
}
.header4 {
  padding: 100px;
  color: red;
  border: 4px solid #c28862;
  margin: -14px;
}
</style>