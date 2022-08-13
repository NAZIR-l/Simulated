<template>
  <div class="containers">
    <div class="btn">
      <button v-if="!ShowS" class="btn btn-secondary shadow-lg" @click="ShowWindowCreate">Decide</button>
      <div v-if="ShowS" class="box">
        <!-- <BOX :Show="ShowS" /> -->
        <div class="header">
          <h3 class="title">Decide</h3>
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

           
                      <label for="TYPE"> TYPE </label><br />
                      <select
                        name="TYPE"
                        v-model="Type"
        
                        @change="onChange($event)"

                      >
                        <option value="TCH">2-way by chance</option>
                        <option value="TCO" >2-way by condition</option>
                        <option value="NCH">n-way by chance</option>
                        <option value="NCO">n-way by condition</option>
                      </select>
                   
              </div>
            </div>
          </div>
        </div>

        <div v-if="TCH" class="border">
          <div class="container">
            <div class="row">
              <div class="col">
                <label for="Action"> Percent true </label><br />
                <select
                  name="Action"
                  v-model="percent"
                  style="width:100px;"
                >
                  <option  value="50">50</option>
                  <option value="60">60 </option>
                  <option value="70">70</option>
                  <option value="80">80</option>
                  <option value="90">90</option>
                  <option value="100">100</option>

                </select>%
              </div>
            </div>
          </div>
        </div>
        <div v-if="TCO" class="Tco">
            
            <div class="container">
                <div class="row">
                <div class="col">
                <label for="Action">it</label><br />
                <select
                  name="Action"
                  v-model="IT"
                  style="width:150px;"
                  @click="COMPARE"
                >
                  <option  value="Variable">Variable</option>
                  <option value="Attribute">Attribute </option>
            
                </select>
              </div>
              <div class="col">
                        <label for="name"> NAME </label><br />
                <input type="text" v-model="NAMEVA" name="" id="name" @click="COMPARE" />
                
           
              </div>
              <div class="col">
                <label for="IS">IS</label><br />
                <select name="IS" v-model="IS" style="width:50px;" >
                  <option  value=">="> >=</option>
                  <option value=">"> ></option>
                  <option value="!"> != </option>
                  <option value="="> == </option>
                </select>
              </div>
              <div class="col">
                        <label for="Value" > Value </label><br />
                <input type="number" style="width:350px;" v-model="Value" name="" id="Value" />
    
              </div>
                </div>
            </div>
        </div>



        <div class="butoon">
          <button @click="ShowWindowCreate" v-on:click="emitToParent">OK</button>
          <button @click="ShowWindowCreate">Cancel</button>
          <button>Help</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import { ref } from "vue";
import BOX from "../Creates/Box.vue";
import { defineComponent, ref } from "vue";

export default defineComponent({
  props:['NameAssign','TypeAssign','ValueAssign'],
  data() {
    return {
      ShowS: false,
      NAME: "Decide 1",
      Type: "",
      percent:"100",
      IT:"Variable",
      Value:1,
      IS:">=",
      NAMEVA:"Variable",
    };
  },
  methods: {
    ShowWindowCreate() {
      this.ShowS= !this.ShowS;
    },   
     emitToParent (event) {
      this.$emit('childToParent',this.percent,this.IT , this.Value,this.IS,this.Type ,this.NAMEVA);
    }, 
    
    COMPARE  () {
    console.log(this.IT)
    console.log(this.TypeAssign)
    if(this.IT == this.TypeAssign ){
this.NAMEVA = this.NameAssign
console.log(this.NAMEVA)
}
if(this.IT == "Attribute"){ 
  this.NAMEVA = "Attribute"
}

  }

  },

  setup(props) {
    let TCO = ref(false);
    let TCH = ref(false);
    const onChange = (e) => {
      //   console.log(e.target.value);
      if (e.target.value === "TCO") {
        TCO.value = true;
        // console.log(SDRE);
      } else {
        TCO.value = false;
      }
  if (e.target.value === "TCH") {
        TCH.value = true;

        // console.log(SDRE);
      } else {
        TCH.value = false;
      }


    };
    const COMPARE = () =>{
    console.log(this.IT)
    console.log(props.TypeAssign)

  }
    const ShowAndADD = () => {};
    return { TCO,TCH, onChange, ShowAndADD };
  },
  
});
</script>

<style>
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
.bton {
  display: flex;
  flex-direction: column;
  align-items: end;
  padding: 12px;
}
</style>