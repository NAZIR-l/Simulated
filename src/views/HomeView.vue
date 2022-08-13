<template>
  <div class="home">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="/">Simulation</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNavDarkDropdown"
          aria-controls="navbarNavDarkDropdown"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="Run" style="padding: 20px 10px">
          <button
            @click="ShowRuns"
            v-on:click="Persent"
            class="btn btn-secondary"
            style="padding: 20px; position: relative; left: 920%"
          >
            RUN
          </button>
        </div>
        <input type="number" name="" v-model="NumbersC" id="" />
        <div class="collapse navbar-collapse" id="navbarNavDarkDropdown">
          <ul class="navbar-nav">
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDarkDropdownMenuLink"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                RUN
              </a>
              <ul
                class="dropdown-menu dropdown-menu-dark"
                aria-labelledby="navbarDarkDropdownMenuLink"
              >
                <li @click="GOSetup">
                  <a class="dropdown-item" href="#">Setup</a>
                </li>
                <li>
                  <a class="dropdown-item" href="#">GO</a>
                </li>
                <li>
                  <a class="dropdown-item" href="#">Fast</a>
                </li>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <div v-if="ShowRun" class="Run">
      <Run
        :Replication="Replication"
        :length="length"
        :maxCreate="SUMCREATE"
        :NameAssign="NameAssign"
        :errorMessage="errorMessage"
        :CONSTVALUE="CONSTVALUE"
        :arrayX="arrayX"
      />
    </div>

    <div class="container" v-if="!ShowRun">
      <div class="BOXED" v-if="ShowS">
        <SetUp v-on:childToParent="onChildClick" />
      </div>

      <div class="container">
        <div class="create">
          <div v-for="Numbered in NumbersC" :key="Numbered" class="create">
            <CREATE
              v-on:childToParent="onChildClickCreate"
              :Numbered="Numbered"
            />
          </div>
        </div>

        <div class="Process">
          <Process v-on:childToParent="onChildClickPro" />
        </div>

        <div class="Decide">
          <Decide
            :NameAssign="NameAssign"
            :TypeAssign="TypeAssign"
            :ValueAssign="ValueAssign"
            v-on:childToParent="onChildClickDEC"
          />
        </div>
        <div class="Assign">
          <Assign v-on:childToParent="onChildClickAssign" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import CREATE from "../components/Creates/Create.vue";
import Process from "../components/Process/Process.vue";
import Decide from "../components/Decide/Decide.vue";
import Assign from "../components/Assign/Assign.vue";
import SetUp from "./setup/SetUp.vue";
import Run from "./Run.vue";
export default {
  name: "HomeView",
  data() {
    return {
      ShowRun: false,
      NumbersC: 1,
      NumbersP: 1,
      ShowS: false,

      Replication: 1,
      length: "",

      typeCreate: "",
      valueCreate: "",
      unitCreate: "",
      maxCreate: "",
      maxCreate2: false,
      numberArrivL: "",

      Delay: "",
      Unit: "",
      Allocation: "",
      minimum: "",
      Value: "",
      maximum: "",

      NameAssign: "",
      ValueAssign: "",
      TypeAssign: "",

      Parcent: "",
      TypeDecide: "",
      ValueDecide: "",
      Operation: "",
      ITDECide: "",
      NAMEVA: "",

      CONSTVALUE: 0,

      SUMCREATE: 0,
      arrayP: [],
      arrayX: [],
      errorMessage: "",
    };
  },
  components: {
    CREATE,
    Process,
    Decide,
    Assign,
    SetUp,
    Run,
  },
  methods: {
    GOSetup() {
      this.ShowS = !this.ShowS;
    },
    ShowRuns() {
      this.ShowRun = !this.ShowRun;
    },
    onChildClick(Replication, length) {
      this.Replication = Replication;
      this.length = length;
    },
    onChildClickCreate(
      typeCreate,
      valueCreate,
      unitCreate,
      maxCreate,
      numberArrivL
    ) {
      this.typeCreate = typeCreate;
      this.valueCreate = valueCreate;
      this.unitCreate = unitCreate;
      this.maxCreate = maxCreate;
      this.numberArrivL = numberArrivL;
      this.arrayP.push(this.maxCreate);
    },
    onChildClickPro(Delay, Unit, Allocation, minimum, Value, maximum) {
      this.Delay = Delay;
      this.Unit = Unit;
      this.Allocation = Allocation;
      this.minimum = minimum;
      this.Value = Value;
      this.maximum = maximum;
    },
    onChildClickAssign(name, value, type) {
      this.NameAssign = name;
      this.ValueAssign = value;
      this.TypeAssign = type;
    },
    onChildClickDEC(parcent, it, value, operation, type, NAMEVA) {
      this.Parcent = parcent;
      this.ValueDecide = value;
      this.Operation = operation;
      this.ITDECide = it;
      this.TypeDecide = type;
      this.NAMEVA = NAMEVA;
    },
    Persent() {
      if (this.typeCreate == "Random") {
        if (this.TypeDecide == "") {
          for (let i = 0; i <= this.Replication; i++) {
            var Random = Math.floor(Math.random() * this.length) + 1;
            this.numberArrivL = this.numberArrivL * Random;
            this.arrayX.push(this.numberArrivL);
            this.numberArrivL = this.numberArrivL / Random;
          }
          console.log(this.arrayX);
          this.SUMCREATE = Math.floor(this.numberArrivL * 6.5);
        } else if (this.TypeDecide == "TCH") {
          for (let i = 0; i < array.length; i++) {
            this.arrayX[i] = (this.numberArrivL * Random * this.Parcent) / 100;
          }
          this.SUMCREATE = this.numberArrivL * (this.length + 1);
        } else if (this.TypeDecide == "TCO") {
          if (this.Operation == ">=") {
            if (this.TypeAssign == this.ITDECide) {
              if (this.NameAssign == this.NAMEVA) {
                if (this.ValueAssign >= this.ValueDecide) {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] =
                      (this.numberArrivL * Random * this.Parcent) / 100;
                  }
                  this.SUMCREATE = this.numberArrivL * (this.length + 1);
                } else {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = 0;
                  }
                  this.SUMCREATE = this.numberArrivL * this.length;
                }
              }
            }
          } else if (this.Operation == "==") {
            if (this.TypeAssign == this.ITDECide) {
              if (this.NameAssign == this.NAMEVA) {
                if (this.ValueAssign == this.ValueDecide) {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] =
                      (this.numberArrivL * Random * this.Parcent) / 100;
                  }
                  this.SUMCREATE = this.numberArrivL * (this.length + 1);
                } else {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = 0;
                  }
                  this.SUMCREATE = this.length - 1;
                }
              }
            }
          } else if (this.Operation == "!=") {
            if (this.TypeAssign == this.ITDECide) {
              if (this.NameAssign == this.NAMEVA) {
                console.log(this.NameAssign);
                console.log(this.NAMEVA);

                if (this.ValueAssign != this.ValueDecide) {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] =
                      (this.numberArrivL * Random * this.Parcent) / 100;
                  }
                } else {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = 0;
                  }
                  this.SUMCREATE = this.length - 1;
                }
              }
            }
          }
        }
      } else if (this.typeCreate == "Constant") {
        let Random = Math.floor(Math.random() * this.length) + 1;
        if (this.TypeDecide == "") {
          for (let i = 0; i <= this.Replication; i++) {
            this.arrayX[i] = this.numberArrivL * (this.length + 1);
          }
          this.SUMCREATE = this.numberArrivL * (this.length + 1);
        } else if (this.TypeDecide == "TCH") {
          for (let i = 0; i < array.length; i++) {
            this.arrayX[i] =
              (this.numberArrivL * (this.length + 1) * this.Parcent) / 100;
          }
          this.SUMCREATE = this.numberArrivL * (this.length + 1);
        } else if (this.TypeDecide == "TCO") {
          if (this.Operation == ">=") {
            if (this.TypeAssign == this.ITDECide) {
              if (this.NameAssign == this.NAMEVA) {
                if (this.ValueAssign >= this.ValueDecide) {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = this.numberArrivL * (this.length + 1);
                  }
                } else {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = 0;
                  }
                  this.SUMCREATE = this.length + 1;
                }
              }
            }
          } else if (this.Operation == "==") {
            if (this.TypeAssign == this.ITDECide) {
              if (this.NameAssign == this.NAMEVA) {
                if (this.ValueAssign == this.ValueDecide) {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = this.numberArrivL * (this.length + 1);
                  }
                } else {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = 0;
                  }
                  this.SUMCREATE = this.length + 1;
                }
              }
            }
          } else if (this.Operation == "!=") {
            if (this.TypeAssign == this.ITDECide) {
              if (this.NameAssign == this.NAMEVA) {
                if (this.ValueAssign != this.ValueDecide) {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = this.numberArrivL * (this.length + 1);
                  }
                } else {
                  for (let i = 0; i < array.length; i++) {
                    this.arrayX[i] = 0;
                  }
                  this.SUMCREATE = this.length + 1;
                }
              }
            }
          }
        }
      }
    },
  },

  // if(){
  //
  //       }

  setup() {
    return;
  },
};
</script>
<style scoped>
.container {
  display: inline-flex;
  padding-top: 150px;
}
.process {
  position: fixed;
  top: -100px;
}
</style>

