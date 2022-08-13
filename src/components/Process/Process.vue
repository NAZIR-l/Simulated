<template>
  <div class="containers">
    <div class="btn">
      <button v-if="!ShowS" class="btn btn-secondary shadow-lg" @click="ShowWindowCreate">{{NAME}}</button>
      <div v-if="ShowS" class="box">
        <!-- <BOX :Show="ShowS" /> -->
        <div class="header">
          <h3 class="title">{{NAME}}</h3>
          <p class="help">?</p>
          <p class="close" @click="ShowWindowCreate">X</p>
        </div>
        <div class="inputs">
          <div class="container">
            <div class="row">
              <div class="col">
                <label for="name"> NAME </label><br />
                <input type="text" v-model="NAME" name="" id="name" />
              </div>
              <div class="col">
                <label for="TYPE"> TYPE </label> <br />
                <input type="text" v-model="TYPE" name="" id="Entity" />
              </div>
            </div>
          </div>
        </div>

        <div class="border">
          <h4>Logic</h4>

          <div class="container">
            <div class="row">
              <div class="col">
                <label for="Action"> Action </label><br />
                <select
                  name="Action"
                  v-model="Actions"
                  @change="onChange($event)"
                >
                  <option value="D">Delay</option>
                  <option value="SD">Seize Delay</option>
                  <option value="SDR">Seize Delay Relase</option>
                  <option value="DR">Delay Relase</option>
                </select>
              </div>

              <div v-if="SDRE" class="col">
                <label for="Priority"> Priority </label><br />
                <select
                  name="Priority"
                  v-model="Prioritys"

                >
                  <option value="High">High(1)</option>
                  <option value="medium">Medium(2)</option>
                  <option value="Low">Low(3)</option>
                </select>
              </div>
            </div>
          </div>

          <div v-if="SDRE" class="bton">
               <div class="textrAREA" v-if="SDRE">
           <textarea v-model="TEXTAREA"  style="position: relative;left: -230px;" rows="6" cols="30"></textarea>

        </div>
        <div style="position: absolute;display: grid;">
   <button @click="ShowAndADD">ADD</button>

            <button>EDITE</button>
            <button>DELETE</button> 
        </div>


         
          </div>
        </div>
     

        <div class="container">
          <div class="row">
            <div class="col">
              <label for="Delay"> Delay Type </label><br />
              <select name="Delay" v-model="Delays" >
                <option value="constants">constants</option>
                <option value="Normal">Normal</option>
                <option value="Uniform">Uniform</option>
                <option value="Triangular">Triangular</option>
                <option value="Expression">Expression</option>
              </select>
            </div>
            <div class="col">
              <label for="UNIT"> UNIT </label><br />
              <select name="UNit" v-model="Unit" >
                <option value="Secounds">Secounds</option>
                <option value="Minutes">Minutes</option>
                <option value="Hours">Hours</option>
                <option value="Days">Days</option>
              </select>
            </div>
            <div class="col">
              <label for="Allocation"> Allocation </label><br />
              <select
                name="Allocation"
                v-model="Allocations"
                
              >
                <option value="VA">value Added</option>
                <option value="NVA">Non_value Added</option>
                <option value="T">Transfer</option>
                <option value="A">Await</option>
                <option value="O">Other</option>
              </select>
            </div>
            <div class="col">
              <label for="Minimum"> Minimum </label><br />
              <input
                type="number"
                style="width: 160px"
                v-model="Minimum"
                name=""
                id="Minimum"
              />
            </div>
            <div class="col">
              <label for="Value"> Value (must likely) </label><br />
              <input
                type="number"
                style="width: 150px"
                v-model="Value"
                name=""
                id="Value"
              />
            </div>
            <div class="col">
              <label for="maximum"> maximum </label> <br />
              <input
                type="number"
                style="width: 150px"
                v-model="maximum"
                name=""
                id="maximum"
              />
            </div>
          </div>
        </div>

        <div class="butoon">
          <button @click="ShowWindowCreate" v-on:click="emitToParent"> OK </button>
          <button @click="ShowWindowCreate">Cancel</button>
          <button>Help</button>
        </div>
      </div>
    </div>
        <div v-if="ShowA" >
<BOX v-on:childToParent="onChildClick"/>
    </div>
  </div>
</template>

<script>
// import { ref } from "vue";
import BOX from "./BOXPRO.vue";
import { defineComponent, ref } from "vue";

export default defineComponent({
  data() {
    return {
      ShowS: false,
      ShowA: false,
      NAME: "Process",
      TYPE: "standard",
      Actions: "D",
      Unit: "Secounds",
      Allocations: "VA",
      Delays: "constants",
      Prioritys: "medium",
      maximum: 1.5,
      TEXTAREA:"<End of list>",
      Value: 1,
      Minimum: 0.5,
      Allocation: "   ",
    TypeBOXPRo:'',
    valueBOXPRo:'',
    SeizePro:'',

    };
  },
  components: {
    BOX,
  },
  methods: {
    ShowWindowCreate() {
      this.ShowS=!this.ShowS;
    },
      ShowAndADD (){
this.ShowA =!this.ShowA;
    },
      emitToParent (event) {
      this.$emit('childToParent',this.Delays,this.Unit,this.Allocation,this.Minimum,this.Value,this.maximum)
    },
    onChildClick(type,value,seize){
this.TypeBOXPRo=type
this.valueBOXPRo=value
this.SeizePro=seize
    }
  },

  setup() {
    let SDRE = ref(false);
    const onChange = (e) => {
      if (e.target.value === "SDR") {
        SDRE.value = true;
      } else {
        SDRE.value = false;
      }
    };
   
    return { SDRE, onChange  };
  },
});
</script>

<style scoped>

.btn {
  padding: 20px;
}
.box {
  height: auto;
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

.butoon {
  padding-top: 15px;
  display: flex;
  justify-content: end;
}
.butoon button {
  margin: 15px;
}
.bton{
    display: flex;
    flex-direction: column;
    align-items: end;
    padding: 12px;
}
</style>