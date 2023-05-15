<template>
  <div
    class="app"
    :class="{
      appMobile: isMobile,
      appTablet: isTablet,
      appDesktop: isDesktop,
    }"
  >
    <div class="header">
      <h2>Лабораторная работа №4</h2>
    </div>
    <div :class="[isDesktop ? 'mainDesktop' : 'mainMobile']" class="main">
      <div
        :class="{
          userInputMobile: isMobile,
          userInputTablet: isTablet,
          userInputDesktop: isDesktop,
        }">
        <dot-form
          class="form appElement"
          :class="[
            isMobile ? 'formMobile' : 'formDesktop',
            isMobile ? 'appElementMobile' : 'appElementDesktop',
          ]"
          @changeR="changeR"
          @create="createDot"
        />
        <my-graph
          class="graph appElement"
          :circles="circles"
          :class="[
            isMobile ? 'formMobile' : 'formDesktop',
            isMobile ? 'appElementMobile' : 'r',
          ]"
          :r="r"
          @create2="createDot"
        ></my-graph>
      </div>
      <div
        :class="{
          userInputMobile: isMobile,
          userInputTablet: isTablet,
          userInputDesktop: isDesktop,
        }"
      >
        <dot-table
          :dots="dots"
          :headerDot="headerDot"
          class="table appElement appElementDesktop"
          @clean="cleanDot"
        />
      </div>
    </div>
  </div>
</template>

<script>
import DotForm from "@/components/DotForm.vue";
import DotTable from "@/components/DotTable.vue";
import MyGraph from "@/components/graph/MyGraph.vue";
import axios from "axios";

export default {
  components: {
    DotTable,
    DotForm,
    MyGraph,
  },
  name: "App",
  data() {
    return {
      isMobile: false,
      isTablet: false,
      isDesktop: false,
      headerDot: {
        id: "id",
        x: "X",
        y: "Y",
        r: "R",
        result: "Result",
        checkTime: "Current time",
        computationTime: "Computation time",
      },
      dots: [],
      circles: [],
      r: 1,
    };
  },
  mounted() {
    this.createDot();
    this.isMobileFunc();
  },
  methods: {
    isMobileFunc() {
      if (document.documentElement.clientWidth <= 300) {
        this.isMobile = true;
        this.isTablet = false;
        this.isDesktop = false;
      } else if (document.documentElement.clientWidth <= 700) {
        this.isMobile = false;
        this.isTablet = true;
        this.isDesktop = false;
      } else {
        this.isMobile = false;
        this.isTablet = false;
        this.isDesktop = true;
      }
    },
    createDot() {
      axios
        .get("http://localhost:8081/api/dots", {
          headers: {
            Authorization: "Bearer " + localStorage.token,
          },
        })
        .then((res) => {
          this.dots = res.data;
        })
        .catch((error) => console.log(error));
      axios
        .get("http://localhost:8081/api/circles/" + this.r, {
          headers: {
            Authorization: "Bearer " + localStorage.token,
          },
        })
        .then((res) => {
          this.circles = res.data;
        })
        .catch((error) => console.log(error));
    },
    cleanDot() {
      axios.delete("http://localhost:8081/api/dots", {
        headers: {
          Authorization: "Bearer " + localStorage.token,
        },
      });
      this.dots = [];
      this.circles = [];
    },
    changeR(r) {
      this.r = r;
      axios
        .get("http://localhost:8081/api/circles/" + this.r, {
          headers: {
            Authorization: "Bearer " + localStorage.token,
          },
        })
        .then((res) => {
          this.circles = res.data;
        })
        .catch((error) => console.log(error));
    },
  },
};
</script>

<style scoped>
*:global(*) {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border-radius: 7px;
  background-color: #d7d4c9;
  font-family: "Courier New";
  font-weight: bolder;
  color: black;
}
.appMobile {
  --text-size: 10px;
  --text-size-header: 20px;
  --padding-size: 5px;
  --button-size: 80px;
  --element-form-text-size: 10px;
}
.appTablet {
  --text-size: 10px;
  --text-size-header: 20px;
  --padding-size: 10px;
  --button-size: 80px;
  --element-form-text-size: 10px;
}
.appDesktop {
  --text-size: 20px;
  --text-size-header: 45px;
  --padding-size: 10px;
  --button-size: 110px;
  --element-form-text-size: 16px;
}
.app {
  width: 100%;
  padding: var(--padding-size);
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}
.userInputMobile {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}
.userInputTablet {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
.userInputDesktop {
  width: 50%;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
.main {
  font-size: var(--text-size);
}
.mainDesktop {
  display: flex;
  justify-content: space-evenly;
  flex-direction: row;
}
.mainMobile {
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
}
.form,
.graph {
  width: 50%;
}

.table,
.formMobile,
.graphMobile {
  width: 100%;
}

.appElement{
  margin: 10px;
  padding: 20px;
  border: 1.5px solid black;
  display: flex;
  flex-direction: column;
}

.appElementDesktop {
  height: 390px;
}

.header {
  width: 100%;
  text-align: center;
  font-size: var(--text-size-header);
  margin: 20px 0px 20px 0px;
}
</style>
