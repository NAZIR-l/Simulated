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
                <label for="Replication"> Number of Replication </label> <br />
                <input type="number" v-model="Replication" name="" id="Replication" />
              </div>
            </div>
          </div>
        </div>

        <div class="border">
         
  

          <div class="container">
            <div class="row">
          
              <div class="col">
                <label for="length">Replication length </label><br />
                <input
                  type="number"
                  v-model="length"
                  name=""
                  style="width: 400px"
                  id="length"
                />
              </div>
         
            </div>
          </div>
        </div>

    

          <div class="butoon">
            <button  @click="ShowWindowCreate" v-on:click="emitToParent"> OK</button>
            <button  @click="ShowWindowCreate"> Cancel</button>
            <button disabled> APPly</button>
            <button> Help</button>

          </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  data() {
    return {
      ShowS: true,
      Replication:1,
      length:1,
     
      onChange(e) {
        console.log(e.target.value);
      },
    };
  },
  components: {
  },
  methods: {
    ShowWindowCreate() {
      this.ShowS =!this.ShowS;
    },
      emitToParent (event) {
      this.$emit('childToParent', this.Replication,this.length)
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