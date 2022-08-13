<template>
  <div class="containers">
    <div class="btn">
      <button v-if="!ShowS" class="btn btn-secondary shadow-lg" @click="ShowWindowCreate">Assign</button>
      <div v-if="ShowS" class="box">
        <!-- <BOX :Show="ShowS" /> -->
        <div class="header">
          <h3 class="title">Assign</h3>
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
            </div>
          </div>
        </div>

        <div class="border">
          <div class="bton">

            <div class="textrAREA">
              <textarea
                v-model="NameBOX"
                style="position: relative; left: -230px; "
                label="Name"
                rows="6"
                cols="30"
              >

              </textarea>
            </div>
            <div style="position: absolute; display: grid ; ">
              <button @click="ShowADD" style="margin:5px;  border-radius: 8px;">ADD</button>
    
              <button  style="margin:5px;border-radius: 8px;">EDITE</button>
              <button  style="margin:5px;border-radius: 8px;">DELETE</button>
            </div>
          </div>
        </div>
        <div class="butoon">
          <button  @click="ShowWindowCreate" v-on:click="emitToParent" >OK</button>
          <button @click="ShowWindowCreate" >Cancel</button>
          <button >Help</button>
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
import { defineComponent, ref } from "vue";
import BOX from '../Assign/BOXes.vue'
export default defineComponent({
  data() {
    return {
      ShowS: false,
      NAME: "Assign 1",
      TEXTAREA: "<End of List>",
      ShowA: false,
      TypeBOX:'',
      ValueBOX:'',
      NameBOX:"",
    };
  },
  components: {
    BOX,
  },
  methods: {
    ShowWindowCreate() {
  this.ShowS =!this.ShowS;      
    },
    ShowADD ()  {
  this.ShowA =!this.ShowA;
    },
    
      onChildClick (type,value,name) {
      this.TypeBOX = type
      this.ValueBOX = value
      this.NameBOX = name
    },
        emitToParent (event) {
      this.$emit('childToParent', this.NameBOX,this.ValueBOX,this.TypeBOX)
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
    return { SDRE, onChange };
  },
});
</script>

<style>
.Boxes{
    z-index: 1000;
}
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
  border-radius: 8px;
}
.bton {
  display: flex;
  flex-direction: column;
  align-items: end;
  padding: 12px;
}

</style>