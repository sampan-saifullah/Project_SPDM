<template>
  <div align="center" color="white" class="pt-4">
    <v-row>
      <v-col class="d-flex" cols="12">
        <v-select
          :items="items"
          label="Select Area"
          dense
          v-model="area"
          @change="loadAreaPost"
        ></v-select>
      </v-col>
    </v-row>
    <v-row class="pa-0 ma-0">
      <v-col
        class="d-flex pa-0 ma-0"
        cols="12"
        sm="6"
        md="4"
        lg="2"
        v-for="i in data"
        :key="i._id"
      >
        <v-card class="ma-4" max-width="344">
          <v-card-text>
            <p class="text-h6 text--primary">{{ i.type }}</p>
            <p>{{ i.area }}</p>
            <div class="text--primary">Price - {{ i.price }} tk</div>
          </v-card-text>
          <v-card-actions>
            <NuxtLink :to="`/info/${i._id}`" style="text-decoration: none">
              <v-btn text color="orange">see More</v-btn>
            </NuxtLink>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data: () => ({
    items: [
      "All",
      "Baridhara",
      "Ghulsan 1",
      "Ghulsan 2",
      "Dhanmondi",
      "Motijheel",
      "Kawran Bazar",
      "Paltan",
      "Banani",
      "Uttara",
      "Mirpur",
      "Bashundhara Residential Area",
      "Panthapath",
      "Maghbazar",
      "Mohakhali",
    ],
    area: "All",
    data: [],
  }),
  mounted() {
    this.loadPost();
  },
  methods: {
    async loadPost() {
      const d = await this.$axios.get("/post");
      this.data = d.data.data;
    },
    async loadAreaPost() {
      if (this.area === "All") {
        this.loadPost();
        return;
      }
      const d = await this.$axios.get("/post/" + this.area);
      this.data = d.data.data;
      console.log(this.area);
    },
  },
};
</script>
<style>
.v-card--reveal {
  bottom: 0;
  opacity: 1 !important;
  position: absolute;
  width: 100%;
}
</style>