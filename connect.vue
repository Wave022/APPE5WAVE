<template>
    <v-container fluid class="pa-5" style="background-color: #f5f5f5;">
      <v-row justify="center">
        <v-col cols="12" md="8">
          <v-card class="elevation-3" max-width="800px">
            <v-card-title class="headline text-center py-4" style="color: #1e88e5;">
              Contact Us
            </v-card-title>
  
            <v-divider></v-divider>
  
            <v-card-text class="px-5 py-3">
              <v-form ref="form" v-model="valid" lazy-validation>
                <v-text-field
                  v-model="name"
                  label="Name"
                  :rules="[v => !!v || 'Name is required']"
                  required
                  outlined
                ></v-text-field>
  
                <v-text-field
                  v-model="email"
                  label="Email"
                  :rules="[v => !!v || 'Email is required', v => /.+@.+/.test(v) || 'E-mail must be valid']"
                  required
                  outlined
                ></v-text-field>
  
                <v-textarea
                  v-model="message"
                  label="Message"
                  :rules="[v => !!v || 'Message is required']"
                  required
                  outlined
                  rows="5"
                ></v-textarea>
  
                <v-row class="text-center pt-4">
                  <v-col>
                    <v-btn color="primary" @click="submit" :disabled="!valid" large>Send Message</v-btn>
                  </v-col>
                </v-row>
              </v-form>
            </v-card-text>
  
            <v-divider></v-divider>
  
            <v-card-actions class="justify-center py-4">
              <v-icon color="primary">mdi-phone</v-icon>
              <span class="mr-4">+123 456 789</span>
              <v-icon color="primary">mdi-email</v-icon>
              <span>66309010026@ccollege.ac.th</span>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: "",
        email: "",
        message: "",
        valid: false,
      };
    },
    methods: {
      submit() {
        if (this.$refs.form.validate()) {
          alert("Message sent successfully!");
          this.clearForm();
        }
      },
      clearForm() {
        this.name = "";
        this.email = "";
        this.message = "";
      },
    },
  };
  </script>
  
  <style scoped>
  .v-card {
    border-radius: 12px;
  }
  
  .v-card-title {
    font-weight: bold;
  }
  
  .v-text-field,
  .v-textarea {
    margin-bottom: 20px;
  }
  
  .v-btn {
    text-transform: none;
  }
  
  .v-card-actions {
    background-color: #f5f5f5;
    font-weight: bold;
    font-size: 1.1rem;
  }
  </style>
  