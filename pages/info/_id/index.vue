<template>
  <div>
    <v-card v-if="!loading" class="mx-auto" max-width="344">
      <v-card-text>
        <p class="text-h4 text--primary">{{ data.type }}</p>
        <p>{{ data.area }}</p>
        <div class="text--primary">{{ data.description }}</div>
      </v-card-text>
      <v-card-actions>
        <v-btn text color="teal accent-4"> Price - {{ data.price }} tk </v-btn>
      </v-card-actions>
      <div class="pa-4">
        <div>Address - {{ data.address }}</div>
        <div>Address - {{ data.phone }}</div>
      </div>
    </v-card>
    <v-card v-else> loading </v-card>
  </div>
</template>
<script>
export default {
  data: () => ({
    data: [],
    loading: true,
  }),
  mounted() {
    console.log(this.$route.params.id);
    this.loadSinglePost();
  },
  methods: {
    async loadSinglePost() {
      const d = await this.$axios.get("/post/id/" + this.$route.params.id);
      if (d.data.data) {
        this.loading = false;
        this.data = d.data.data;
      }
      console.log(this.data);
    },
  },
};
</script>