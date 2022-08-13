<template>
  <div class="containers">
    <div class="btn">
      <button v-if="!ShowS" class="btn btn-secondary shadow-lg" @click="ShowWindowCreate">{{NAME}}</button>
      <div v-if="ShowS" class="box">
        <div class="header">
          <h3 class="title">{{NAME}}</h3>
          <p class="help">?</p>
          <p class="close" @click="ShowWindowCreate">X</p>
        </div>
        <div class="inputs">
          <div class="container">
            <div class="row">
              <div class="col">
                <label for="Nfname"> NAME </label><br />
                <input type="text" v-model="NAME" name="" id="Nfname" />
              </div>
              <div class="col">
                <label for="Entity"> Entity type </label> <br />
                <input type="text" v-model="Entity" name="" id="Entity" />
              </div>
            </div>
          </div>
        </div>

        <div class="border">
          <h4>Time Between Arrival</h4>
          <br />

          <div class="container">
            <div class="row">
              <div class="col">
                <label for="TYPE"> TYPE </label><br />
                <select name="TYPE" v-model="Type" @change="onChange($event)">
                  <option value="Random">Random (EXOP)</option>
                  <option value="Schedule">Schedule</option>
                  <option value="Constant">Constant</option>
                  <option value="Expression">Expression</option>
                </select>
              </div>
              <div class="col">
                <label for="VALUE"> VALUE </label><br />
                <input
                  type="number"
                  v-model="VALUE"
                  name=""
                  style="width: 100px"
                  id="VALUE"
                />
              </div>
              <div class="col">
                <label for="UNIT"> UNIT </label><br />
               <select name="UNit"  v-model="Unit" @change="onChange($event)">
                  <option value="Secounds">Secounds</option>
                  <option value="Minutes">Minutes</option>
                  <option value="Hours">Hours</option>
                  <option value="Days">Days</option>
                </select>
              </div>
            </div>
          </div>
        </div>

        <div class="container">
            <div class="row">
              <div class="col">
                <label for="Entites"> Entites per Arrival </label><br />
                <input type="number" v-model="numberArrivL" name="" id="Entites" />
              </div>
              <div class="col">
                <label for="MaxA"> Max Arrival </label> <br />
                <input type="number" v-model="MazArrival" name="" id="MaxA" />
              </div>
            </div>
          </div>

          <div class="butoon">
            <button  @click="ShowWindowCreate" v-on:click="emitToParentCREATE" > OK</button>
            <button  @click="ShowWindowCreate"> Cancel</button>
            <button> Help</button>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import BOX from "../Creates/Box.vue";
export default {
  data() {
    return {
      ShowS: false,
      NAME: "Create",
      Entity: "Entity 1",
      MazArrival:145,
      VALUE:1 ,
      Unit:  "Secounds",
      Type:"Random",
      numberArrivL : 1,
      Arrays:[],
      EQUALT:0,
      onChange(e) {
        console.log(e.target.value);
      },
    };
  },
  components: {
    BOX,
  },
  methods: {
    ShowWindowCreate() {
      this.ShowS=!this.ShowS;
    
    },
      emitToParentCREATE (event) {
        // this.Arrays.push(this.MazArrival)
        this.EQUALT = this.MazArrival
         this.Arrays.push(this.EQUALT)

        console.log(this.Arrays)
      this.$emit('childToParent', this.Type,this.VALUE,this.Unit,this.MazArrival , this.numberArrivL)
    }
  },
};
</script>

<style>
.btn {
  padding: 20px;
}
.box {
  height: 320px;
  width: 550px;
  background-color: rgb(218, 218, 218);
  border-radius: 13px;
}
input {
  size: 12px;
}
.header {
  position: relative;
  height: 30px;
  background-color: #f2f2f2;
  align-items: center;
  text-align: center;
  display: flex;
  justify-content: start;
}
.close {
  display: flex;
  position: absolute;
  right: 0;
  height: 5px;
  width: 5px;
  text-align: center;
  /* top: -15px; */
  overflow: hidden;
  border-radius: 13px;
  padding: 15px;
  justify-content: center;
  align-items: center;
}
.close:hover {
  background-color: red;
}
.help {
  position: absolute;
  right: 65px;
}

.butoon{
    padding-top: 15px;
    display: flex;
    justify-content: end;
    }
    .butoon button{
      margin: 15px;
    }
</style>