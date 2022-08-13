<template>
  <div class="container">
    <div class="btn">
      <div v-if="ShowS" class="box">
        <!-- <BOX :Show="ShowS" /> -->
        <div class="headeq">
          <h3 class="title">Assignments</h3>
       
        </div>
        <div class="inputs">
          <div class="container">
            <div class="row">
              <div class="col">
                <label for="Type">Type  </label><br />
 <select
                  name="Type"
                  v-model="Type"
                  style="width:150px;"
                >
                  <option  value="Variable">Variable</option>
                  <option value="Attribute">Attribute </option>
            
                </select>             
                 </div>
              <div class="col">
                <label for="Type"> Variable Name </label> <br />
                <input type="text" v-model="NAME" name="" id="Type" />
              </div>
            </div>
          </div>
        </div>

        <div class="border">
         
  

          <div class="container">
            <div class="row">
          
              <div class="col">
                <label for="VALUE">New VALUE </label><br />
                <input
                  type="number"
                  v-model="VALUE"
                  name=""
                  style="width: 400px"
                  id="VALUE"
                />
              </div>
         
            </div>
          </div>
        </div>

    

          <div class="butoon">
            <button  @click="ShowWindowCreate" v-on:click="emitToParent"> OK</button>
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
      ShowS: true,
      NAME:'Variable ',
      Type:"Variable",
      VALUE:1,
     
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
     this.ShowS = !this.ShowS;     
    },
    emitToParent (event) {
      this.$emit('childToParent', this.Type,this.VALUE,this.NAME)
    }

  },
};
</script>

<style scoped>
.btn {
  /* padding: 20px; */
  position: absolute;
    z-index: 1000;
    top: 320px;
    left: 0;
    border: solid 2px white;
    background: azure;
    height: auto;
}
.box {
  height: 320px;
  width: 550px;
  background-color: rgb(117, 113, 113);
  border-radius: 13px;
}
input {
  size: 12px;
}
.header {
  position: relative;
  height: 30px;
  background-color: #6b2626;
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