<template>
  <main role="main" class="container">

    <h1>Nano Live Energy Usage</h1>

    <div class="row mb-3">
      <div class="col-4">
          <div class="card">
              <div class="card-body">
                  <h5 class="card-title">{{blockCount}} Blocks</h5>
                  <h6 class="card-subtitle text-muted">Current Blockcount</h6>
              </div>
          </div>
      </div>
    </div>

    <div class="row mb-3">
      <div class="col-4">
          <div class="card">
              <div class="card-body">
                  <h5 class="card-title">{{watthours_all}} Wh</h5>
                  <h6 class="card-subtitle text-muted">Energy Consumption</h6>
              </div>
          </div>
      </div>
      <div class="col-4">
          <div class="card">
              <div class="card-body">
                  <h5 class="card-title">{{watthours_all / 1000}} kWh</h5>
                  <h6 class="card-subtitle text-muted">Energy Consumption</h6>
              </div>
          </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  components: {
    HelloWorld
  },
  data: function() {
    return {
      blockCount: Number
    };
  },
  computed: {
    // a computed getter
    watthours_all: function () {
      // `this` points to the vm instance
      return this.blockCount * 0.0555
    }
  },
  methods: {
    getBlockCount: function() {
      axios.get("https://api.nanocrawler.cc/block_count").then(
        response => {
          this.blockCount = response.data.blockCount.count;
        },
        error => {
          console.log(error);
        }
      );
    }
  },
  mounted: function() {
    this.getBlockCount();
    setInterval(this.getBlockCount, 1500);
  }
};
</script>
