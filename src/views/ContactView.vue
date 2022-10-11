<template>
  <div class="about"  fill-width>
    <div class="contactForm" style="padding: 2rem">
      <v-text-field label="Name of your meal" v-model="name"></v-text-field>
      <v-text-field label="Instructions" v-model="instructions"></v-text-field>
      <v-btn elevation="2" mx="4" @click="showMessage()">Submit</v-btn>
      <v-alert class="message" style="margin: 2rem 0;" type="success" v-if="showSuccess"
        >Success</v-alert>
      <v-alert class="message" style="margin: 2rem 0;" type="error" v-if="showError"
        >Something is not good. Try again!</v-alert>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showError: false,
      showSuccess: false,
      name: "",
      instructions: "",
    };
  },
  methods: {
    showMessage() {
      if (this.name != "" && this.instructions != "") {
        this.showSuccess = true;
        setTimeout(() => {
          this.showSuccess = false;
        }, 2000);
      } else {
        this.showError = true;
        setTimeout(() => {
          this.showError = false;
        }, 2000);
      }
    },
  },
};
</script>

<style scoped>
  .about{
    background-color: rgb(148, 155, 145);
  }
</style>

