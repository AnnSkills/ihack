<template>
  <div>
    <v-container v-if="!createNewWindow" class="pt-10">
      <h2>You can create new company here</h2>
      <v-btn id="buttonClick" outlined rounded text @click="createNewCompany">
        Create new Company
      </v-btn>
    </v-container>
    <v-container v-else>
      <v-card class="mx-auto d-flex flex-row-reverse" width="100%" outlined>
        <v-card-actions>
          <v-container max-width="300">
            <form class="d-flex flex-column">
              <v-text-field required id="userText" v-model="name"  label="Name company"></v-text-field>
              <v-text-field
                id="linkIn" 
                v-model="link"
                label="Link video"
                clearable
              ></v-text-field>
              <v-textarea
                id="middleText"
                clearable
                v-model="description"
                clear-icon="mdi-close-circle"
                label="Text"
                value="This is clearable text."
              ></v-textarea>

              <v-btn id="buttonClick" class="mr-4" @click="submitBIO"> Create </v-btn>
            </form>
          </v-container>
        </v-card-actions>
        <v-container class="d-flex flex-column">
          <h1>{{ name }}</h1>
          <h3>{{ description }}</h3>
        </v-container>
      </v-card>
    </v-container>
    <v-container v-if="!createNewWindow" d-flex flex-row flex-wrap>
      <v-card
        v-for="(company, index) in $store.state.companies"
        :key="index"
        class="mb-10 mr-10"
        max-width="344"
        outlined
      >
        <v-list-item three-line>
          <v-list-item-content>
            <v-list-item-title class="text-h5 mb-1">
              {{ company.name }}
            </v-list-item-title>
            <v-list-item-subtitle>
              {{ company.description }}
            </v-list-item-subtitle>
          </v-list-item-content>

          <v-list-item-avatar tile size="80" color="green"
            >LOGO</v-list-item-avatar
          >
        </v-list-item>

        <v-card-actions>
          <v-btn id="buttonClick" outlined rounded text @click="overview(index)">
            Overview
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-container>
  </div>
</template>
<script>
export default {
  data: () => ({
    createNewWindow: false,
    description: null,
    name: null,
    link: null,
  }),
  methods: {
    createNewCompany() {
      this.$emit("craete"); //hide upper blocks
      this.createNewWindow = !this.createNewWindow;
    },
    submitBIO() {
      console.log("submitBIO");
      this.$store.commit("setCompany", {
        name: this.name,
        link: this.link,
        description: this.description,
        vacancy: [],
      });
      this.name = null;
      this.description = null;
      this.link = null;

      this.createNewWindow = !this.createNewWindow;
    },
    overview(index) {
      console.log("index: ", index);
      this.$router.push(`/dashboard/company/${index}`);
    },
  },
};
</script>
<style>
#userText{
  font-size: 35px;
  font-weight: bold;
}
#linkIn{
  color:blue;
  font-size: 25px;
}
#middleText{
  font-size: 20px;

}
#buttonClick{
  background-color: white;
  color: black;
  border: 2px solid #4CAF50;
  border-radius: 6px;
  margin-top: 10px;
}
</style>
