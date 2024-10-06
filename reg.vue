<template>
    <div>
      <v-img
        class="mx-auto my-6"
        max-width="150"
        src="https://www.logolynx.com/images/logolynx/a6/a60635561d41eceb9cb2411cc7648b81.jpeg"
      ></v-img>
  
      <v-card
        class="mx-auto pa-12 pb-8"
        elevation="8"
        max-width="448"
        rounded="lg"
      >
        <div class="text-subtitle-1 text-medium-emphasis">Register</div>
  
        <!-- Username Field -->
        <v-text-field
          v-model="username"
          density="compact"
          placeholder="Username"
          prepend-inner-icon="mdi-account-outline"
          variant="outlined"
        ></v-text-field>
  
        <!-- Email Field -->
        <v-text-field
          v-model="email"
          density="compact"
          placeholder="Email address"
          prepend-inner-icon="mdi-email-outline"
          variant="outlined"
        ></v-text-field>
  
        <div class="text-subtitle-1 text-medium-emphasis">Password</div>
  
        <!-- Password Field -->
        <v-text-field
          v-model="passwd"
          :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
          :type="visible ? 'text' : 'password'"
          density="compact"
          placeholder="Enter your password"
          prepend-inner-icon="mdi-lock-outline"
          variant="outlined"
          @click:append-inner="visible = !visible"
        ></v-text-field>
  
        <!-- Confirm Password Field -->
        <v-text-field
          v-model="confirmPasswd"
          :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
          :type="visible ? 'text' : 'password'"
          density="compact"
          placeholder="Confirm your password"
          prepend-inner-icon="mdi-lock-outline"
          variant="outlined"
          @click:append-inner="visible = !visible"
        ></v-text-field>
  
        <!-- Register Button -->
        <v-btn
          class="mb-8"
          size="large"
          variant="tonal"
          block
          @click="doRegister"
        >
          Register
        </v-btn>
  
        <!-- Login Link -->
        <v-card-text class="text-center">
          Already have an account? 
          <a
            class="text-blue text-decoration-none"
            href="login"
            @click="goToLogin"
          >
            Log in <v-icon icon="mdi-chevron-right"></v-icon>
          </a>
        </v-card-text>
      </v-card>
    </div>
  </template>
  
  <script>
  definePageMeta({
    layout: "#",
  });
  import axios from 'axios';
  
  export default {
    data: () => ({
      visible: false,
      username: '',
      email: '',
      passwd: '',
      confirmPasswd: ''
    }),
    methods: {
      async doRegister() {
        if (!this.username) {
          alert('Please enter your username.');
          return;
        }
        if (!this.email) {
          alert('Please enter your email address.');
          return;
        }
        if (!this.passwd) {
          alert('Please enter your password.');
          return;
        }
        if (this.passwd !== this.confirmPasswd) {
          alert('Passwords do not match.');
          return;
        }
  
        let forms = {
          username: this.username,
          email: this.email,
          password: this.passwd
        };
  
        try {
          const response = await axios.post('http://localhost:7000/insert', forms);
          const data = response.data;
          if (data.ok) {
            console.log('Registration successful, user ID:', data.id);
            this.$router.replace('/login');
          } else {
            console.error('Registration failed');
          }
        } catch (error) {
          console.error('Error registering:', error);
        }
      },
      goToLogin() {
        this.$router.push('/login');
      }
    }
  };
  </script>

<style scoped>
  /* ปรับปรุงสไตล์ของปุ่ม */
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

/* ลิงก์ไปยังหน้าล็อกอิน */
a.text-blue {
  color: #1e88e5 !important;
  transition: color 0.3s ease;
}

a.text-blue:hover {
  color: #1565c0 !important; /* เปลี่ยนเป็นสีน้ำเงินเข้มขึ้นเมื่อ hover */
}

/* ปรับปรุงสไตล์ของ input fields */
.v-text-field {
  border-color: #1e88e5 !important; /* สีขอบน้ำเงิน */
  transition: border-color 0.3s ease;
}

.v-text-field:hover .v-input__control {
  border-color: #1565c0 !important; /* ขอบเข้มขึ้นเมื่อ hover */
}

/* ปรับปรุงไอคอน */
.v-icon {
  color: #1e88e5 !important;
  transition: color 0.3s ease;
}

.v-icon:hover {
  color: #1565c0 !important; /* สีไอคอนเข้มขึ้นเมื่อ hover */
}

/* ปรับปรุงพื้นหลังของการ์ด */
.v-card {
  background-color: #f5f5f5 !important; /* พื้นหลังสีเทาอ่อน */
  border-radius: 12px !important; /* ขอบโค้งมน */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1) !important; /* เพิ่มเงาเบา ๆ */
}
</style>
    
  
  
  