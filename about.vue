<template>
  <v-container fluid class="pa-5" style="background-color: #f5f5f5;">
    <v-row justify="center">
      <v-col cols="12" md="8">
        <v-card class="elevation-3" max-width="2000px">
          <v-img
            src="https://scontent.fbkk12-2.fna.fbcdn.net/v/t39.30808-6/320341915_466369662323610_1294700008110803652_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=86c6b0&_nc_ohc=n3Wtr_h4Ql0Q7kNvgEW5YKI&_nc_ht=scontent.fbkk12-2.fna&oh=00_AYDbCQ9_qdoxpLwNSuH5h36csnaJiYhJnQhTBZ0OF9SuRg&oe=66DA5E40"
            alt="About Us Image"
            height="300px"
            class="elevation-1"
          ></v-img>

          <v-card-title class="headline text-center py-4" style="color: #1e88e5;">
             เกี่ยวกับเรา
          </v-card-title>

          <v-divider></v-divider>

          <v-card-text class="px-5 py-3">
            <v-row>
              <v-col cols="12">
                <p>
                  สวัสดีครับ ผมชื่อ Nattapon Sappong ผมเป็นนักพัฒนาซอฟต์แวร์ที่มีความหลงใหลในเทคโนโลยีและการเขียนโปรแกรมมาตั้งแต่เริ่มเข้าสู่สายงานนี้ การเขียนโปรแกรมสำหรับผมไม่ใช่เพียงแค่การเขียนโค้ดหรือสร้างโปรแกรมให้ทำงานได้เท่านั้น แต่เป็นการแก้ปัญหาและสร้างสรรค์สิ่งใหม่ๆ ที่สามารถตอบสนองต่อความต้องการของผู้ใช้งานในโลกที่เปลี่ยนแปลงไปอย่างรวดเร็ว
                  ผมมีประสบการณ์ในการพัฒนาโปรแกรมที่หลากหลาย ทั้งในด้านการสร้างแอปพลิเคชันเว็บและมือถือ การพัฒนาระบบ Backend ที่มั่นคง และการทำงานร่วมกับทีมเพื่อส่งมอบโซลูชันที่มีประสิทธิภาพและใช้งานง่าย ผมมุ่งมั่นที่จะเรียนรู้เทคโนโลยีใหม่ๆ และติดตามเทรนด์การพัฒนาโปรแกรมอย่างต่อเนื่อง เพื่อให้แน่ใจว่างานของผมจะอยู่ในระดับที่ทันสมัยและตอบโจทย์ผู้ใช้งานได้ดีที่สุด
                </p>
                <p>
                  นอกจากการเขียนโปรแกรมแล้ว ผมยังชื่นชอบการแบ่งปันความรู้และประสบการณ์กับผู้อื่น ผ่านการทำงานร่วมกันในโปรเจกต์ต่างๆ และการช่วยเหลือทีมในการแก้ไขปัญหาที่ซับซ้อน ผมเชื่อว่าความสำเร็จในการพัฒนาซอฟต์แวร์ไม่ได้มาจากความสามารถของคนคนเดียว แต่เป็นผลจากความร่วมมือและการสื่อสารที่ดีระหว่างทีม
                  ผมพร้อมที่จะนำความรู้และประสบการณ์ที่มีมาช่วยสร้างสรรค์โปรเจกต์ใหม่ๆ ที่สามารถทำให้โลกดิจิทัลนี้ดียิ่งขึ้น ขอบคุณที่ให้ความสนใจครับ"
                </p>
              </v-col>

              <v-col cols="12">
                <v-card class="elevation-2" color="#e3f2fd" outlined>
                  <v-card-title class="headline" style="color: #1976d2;">
                    Our Mission
                  </v-card-title>
                  <v-card-text>
                    พันธกิจของเราคือการสร้างแพลตฟอร์ม E-commerce ที่เข้าถึงง่ายและทรงพลัง ซึ่งช่วยให้ผู้ใช้สามารถควบคุมประสบการณ์การช้อปปิ้งของตนได้อย่างเต็มที่ด้วยเทคโนโลยีที่ใช้งานง่ายและเชื่อถือได้
                  </v-card-text>
                </v-card>
              </v-col>

              <v-col cols="12" class="text-center pt-4">
                <v-btn color="primary" @click="home" class="mr-4" large>ไปยังหน้าหลัก</v-btn>
                <v-btn color="secondary" @click="contactUs" large>ติดต่อเรา</v-btn>
              </v-col>
            </v-row>
          </v-card-text>

          <v-divider></v-divider>

          <v-card-actions class="justify-center py-4">
            <v-btn icon @click="share">
              <v-icon>mdi-share-variant</v-icon>
            </v-btn>
            <v-btn icon @click="like">
              <v-icon>mdi-thumb-up</v-icon>
            </v-btn>
            <v-btn icon @click="follow">
              <v-icon>mdi-account-plus</v-icon>
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
    home() {
      this.$router.push("/home");
    },
    contactUs() {
      alert("Contact us at: contact@example.com");
    },
    share() {
      alert("Share this page!");
    },
    like() {
      alert("You liked this page!");
    },
    follow() {
      alert("You are now following us!");
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

.v-card-text p {
  font-size: 1.2rem;
  line-height: 1.8;
}

.v-btn {
  text-transform: none;
}

.v-card-actions {
  background-color: #f5f5f5;
}

.v-btn v-icon {
  color: #1976d2;
}
</style>
