<template>
    <v-container>
      <v-row>
        <v-col cols="12">
          <v-card>
            <v-card-title>
              ยินดีต้อนรับสู่พื้นที่สร้างสรรค์ของผม!
            </v-card-title>
            <v-card-text>
              ขอบคุณที่สละเวลามาเยี่ยมชมเว็บไซต์พอร์ตโฟลิโอนี้ ที่นี่คุณจะได้พบกับผลงานที่ผมได้สร้างสรรค์ขึ้นด้วยความตั้งใจและความหลงใหลในงานออกแบบและพัฒนา ไม่ว่าจะเป็นโปรเจกต์ทางด้านเว็บไซต์ งานออกแบบกราฟิก หรือโปรเจกต์ส่วนตัวอื่นๆ ทุกชิ้นงานล้วนสะท้อนถึงความพยายามและความมุ่งมั่นในการสร้างสิ่งที่มีคุณค่าและเป็นประโยชน์
              หากคุณสนใจในผลงานหรือมีข้อสงสัยเพิ่มเติม อย่าลังเลที่จะติดต่อผมมาได้เสมอ ไม่ว่าจะเป็นการพูดคุยแลกเปลี่ยนไอเดีย ความร่วมมือในโปรเจกต์ใหม่ หรือแค่ต้องการทำความรู้จัก ผมยินดีเป็นอย่างยิ่งที่ได้รู้จักคุณ
              ขอให้คุณสนุกกับการสำรวจเว็บไซต์นี้ และหวังว่าจะได้มีโอกาสร่วมงานกับคุณในอนาคตครับ!
            </v-card-text>
            <v-card-text>
              Welcome to my creative space! <br>
              Thank you for taking the time to visit this portfolio website. Here, you'll find the works I've passionately crafted, whether it's website projects, graphic design, or other personal endeavors. Every piece reflects my dedication and commitment to creating valuable and meaningful work.
              If you're interested in my work or have any questions, don't hesitate to reach out. Whether it's to exchange ideas, collaborate on a new project, or simply get to know each other, I'm always open to connecting.
              Enjoy exploring this site, and I look forward to the possibility of working with you in the future!
            </v-card-text>
            

            <v-card-actions>
              <v-btn color="primary" @click="about">
                About Us
              </v-btn>
              <v-btn color="secondary" @click="data">
                Members
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    methods: {
      about() {
        this.$router.push('/about');
      },

      data() {
        this.$router.push('/data_table');
      },

      logOut() {
        window.sessionStorage.clear();
        this.$router.replace("/login");
      },
    },
  };
  </script>
  
  <style scoped>
  .v-container {
    margin-top: 20px;
  }
  </style>
  