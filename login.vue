<template>
  <div class="d-flex flex-column align-center justify-center min-vh-100">
    <v-card
      class="mx-auto py-6 px-8"
      elevation="15"
      rounded="lg"
    >
      <v-img
        class="mx-auto mb-8"
        max-width="150"
        src="\public\assets\images\css3-logo-png-transparent.png"
      ></v-img>

      <div class="text-h5 mb-8 text-center">
        Welcome Back
      </div>

      <v-text-field
        v-model="email"
        label="Email Address"
        class="custom-text-field mb-6"
        :error="emailError"
        :error-messages="emailErrorMessages"
      ></v-text-field>

      <v-text-field
        v-model="passwd"
        label="Password"
        :type="visible ? 'text' : 'password'"
        class="custom-text-field mb-6"
        @click:append-inner="visible = !visible"
        :error="passwdError"
        :error-messages="passwdErrorMessages"
      ></v-text-field>
      

      <v-btn
        color="primary"
        size="large"
        variant="contained"
        block
        @click="doLogin"
      >
        <p>Log In</p>
      </v-btn>

      <v-divider class="my-6"></v-divider>

      <v-card-text class="text-center">
        <span>Don't have an account?</span>
        <a
          class="text-blue text-decoration-none"
          rel="noopener noreferrer"
          target="_blank"
          @click="goToRegister"
        >
          Register
        </a>
      </v-card-text>
    </v-card>
  </div>
</template>


<script>
import axios from 'axios'

definePageMeta({
  layout: 'minimal'
});

export default {
  data: () => ({
    visible: false,
    email: '',
    passwd: '',
    emailError: false,
    emailErrorMessages: '',
    passwdError: false,
    passwdErrorMessages: ''
  }),
  methods: {
    async doLogin() {
      // Basic validation
      this.emailError = !this.email;
      this.emailErrorMessages = this.email ? '' : 'Email is required';
      
      this.passwdError = !this.passwd;
      this.passwdErrorMessages = this.passwd ? '' : 'Password is required';
      
      if (this.emailError || this.passwdError) return;

      let forms = {
        email: this.email,
        passwd: this.passwd
      }

      try {
        const response = await axios.post('http://localhost:7000/login', forms)
        const data = response.data

        if (data.status == 'success') {
          window.sessionStorage.setItem("token", JSON.stringify(data.token));
          this.$router.replace('/data_table')
        } else {
          this.$router.replace('/login')
        }
      } catch (error) {
        console.error("Login error:", error);
      }
    },
    goToRegister() {
      this.$router.push('/reg');
    },
  }
};
</script>

<style scoped>
/* ปรับสีพื้นหลังและบัตร */
.v-card {
  background-color: #ffffff;
  border-radius: 16px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  max-width: 400px; /* ปรับขนาดความกว้างของบัตร */
  padding: 24px;
}

/* เพิ่มเงาให้บัตรเมื่อมีการโฮเวอร์ */
.v-card:hover {
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

/* ปรับสีพื้นหลังปุ่มและข้อความ */
.v-btn {
  background-color: #2965c0; /* สีม่วง */
  color: #ffffff; /* ขาว */
  font-weight: bold;
  transition: background-color 0.3s, transform 0.2s;
}

/* เปลี่ยนสีปุ่มเมื่อโฮเวอร์ */
.v-btn:hover {
  background-color: #4790ff; /* สีม่วงเข้ม */
  box-shadow:0px 0px 10px 5px #4790ff;
  transform: scale(1.02); /* ขยายปุ่มเล็กน้อยเมื่อโฮเวอร์ */
}

/* ปรับขนาดและสีของข้อความในบัตร */
.text-h5 {
  font-weight: bold;
  font-size: 24px;
  color: #2965c0; /* สีม่วง */
}

/* ปรับสีของลิงก์ */
a {
  color: #6200ea; /* สีม่วง */
  transition: color 0.3s;
}

/* เปลี่ยนสีลิงก์เมื่อโฮเวอร์ */
a:hover {
  color: #3700b3; /* สีม่วงเข้ม */
}

/* ปรับขนาดและสไตล์ของช่องป้อนข้อมูล */
.custom-text-field {
  width: 100%;
  max-width: 350px;
  height: 50px;
  margin-bottom: 24px;
}

.v-text-field .v-input__control {
  font-size: 14px;
  height: 50px;
}

.v-text-field .v-input__slot {
  padding: 0 12px;
}

/* ปรับสไตล์การจัดตำแหน่ง */
.min-vh-100 {
  min-height: 100vh !important;
}

.d-flex {
  display: flex !important;
}

.flex-column {
  flex-direction: column !important;
}

.align-center {
  align-items: center !important;
}

.justify-center {
  justify-content: center !important;
}

.mb-6 {
  margin-bottom: 24px;
}

.mb-8 {
  margin-bottom: 24px;
}

.my-6 {
  margin: 24px 0;
}
 p{
  color: #ffffff;
 }
</style>

