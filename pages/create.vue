<template>
  <div align="center" color="white" class="pt-4">
    Create New Parking
    <v-row>
      <v-col class="d-flex" cols="4">
        <v-select
          :items="items"
          label="Select Type"
          dense
          v-model="type"
        ></v-select>
      </v-col>
      <v-col class="d-flex" cols="4">
        <v-select
          :items="itemsArea"
          label="Select Area"
          dense
          v-model="area"
        ></v-select>
      </v-col>
      <v-col class="d-flex" cols="4">
        <v-text-field
          label="Price"
          type="number"
          v-model="price"
        ></v-text-field>
      </v-col>
      <v-col class="d-flex" cols="4">
        <v-text-field
          label="Address"
          hide-details="auto"
          v-model="address"
        ></v-text-field>
      </v-col>
      <v-col class="d-flex" cols="4">
        <v-text-field
          label="Phone"
          v-model="phone"
          hide-details="auto"
        ></v-text-field>
      </v-col>
      <v-col class="d-flex" cols="4">
        <v-textarea
          label="Details"
          hide-details="auto"
          v-model="description"
        ></v-textarea>
      </v-col>
    </v-row>
    {{ msg }}
    <div class="pt-4" >
      <v-btn
        @click="savePost"
        block
        :loading="loading"
        :disabled="
          !type || !price || !area || !phone || !description || !address
        "
      >
        Save
      </v-btn>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    msg: "",
    items: ["Private Car", "Bike", "Others"],
    type: "",
    price: 0,
    area: "",
    phone: "",
    description: "",
    address: "",
    itemsArea: [
      "Baridhara",
      "Dhanmondi",
      "Ghulsan 1",
      "Ghulsan 2",
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
    loading: false,
  }),
  methods: {
    savePost() {
      this.loading = true;
      const that = this;
      this.$axios
        .post("/post", {
          type: this.type,
          price: this.price,
          area: this.area,
          phone: this.phone,
          description: this.description,
          address: this.address,
        })
        .then(function (response) {
          console.log(response);
          that.msg = response.data.msg;
          that.type = "";
          that.price = 0;
          that.area = "";
          that.price = "";
          that.phone = "";
          that.description = "";
          that.address = "";
          that.loading = false;
        });
    },
  },
};
</script>

<style>
</style>