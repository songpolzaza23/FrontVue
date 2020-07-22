<template>
  <div id="home">
    <v-container>
      <h1>ส่วนที่ 1</h1>
      <h2>การสุ่มตัวเลขและเคลียตัวเลข</h2>
      <br />
      <v-btn @click="onClickRandom" class="mr-5">RANDOM</v-btn>
      <v-btn @click="onClickClear" class="mr-5">CLEAR</v-btn>
      <v-container>
        <TableList :headers="headers" :desserts="desserts" />
      </v-container>
      <br />
      <h1>ส่วนที่ 2</h1>
      <h2>คำนวนหาค่าที่หารเหลือเศษเท่ากับ 0</h2>
      <br />
      <v-container>
        <v-row
          class="d-flex flex-row"
          v-for="(item, index) in dv.ar1"
          :key="index"
        >
          <span>{{ item.nm1 }} หาร {{ item.nm2 }} ลงตัว</span>
        </v-row>
      </v-container>
      <v-btn @click="onClickDivide" class="mr-5">CALCULATE</v-btn>
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
import TableList from "@/components/TableList.vue";
// import DivideList from "@/components/DivideList.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    TableList,
  },
  async mounted() {
    let result = await axios.get("http://localhost:80");
    this.desserts = result.data.data;
  },
  methods: {
    async onClickRandom() {
      let result = await axios.get("http://localhost:80/api/random");
      this.desserts = result.data.data;
      location.reload();
    },
    async onClickClear() {
      let result = await axios.get("http://localhost:80/api/clear");
      this.desserts = result.data.data;
      location.reload();
    },
    async onClickDivide() {
      let result = await axios.get("http://localhost:80/api/divide");
      this.dv = result.data;
      console.log(this.dv.ar1);
    },
  },
  data() {
    return {
      headers: [
        {
          text: "Order",
          align: "start",
          sortable: false,
          value: "id",
        },
        { text: "Number", value: "number" },
      ],
      desserts: [],
      dv: [],
    };
  },
};
</script>
