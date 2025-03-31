<template>
  <div id="body"> 
  <div id="card"> 
    <div id="head">
      <div id="left" class="card">
        <img src="../assets/images/me1.jpg"/>
      </div>
      <div id="right" class="card">
        <p>{{ student.first_name }} {{ student.last_name }}</p>
        <p>รหัสนิสิต {{ student.student_id }}</p>
        <p>{{ student.major }} at Kasetsart University</p>
        <p>old school at {{ student.school }}</p>
      </div>
    </div>
    
    <div id="foot">
      <div id="left">
        <img v-for="(heart, index) in 10" :key="index" src="../assets/images/heart.png" />
      </div>
      <div id="right">
        <img v-for="(food, index) in 10" :key="index" src="../assets/images/food.png" />
      </div>
    </div>
    
    <div class="text-center mt-3">
      <button @click="toggleEdit" class="btn btn-primary">Edit</button>
    </div>
  
    <div v-if="editMode" class="edit-block p-6 shadow bg-light" id="edit-block">
  <div class="mb-3">
    <label class="form-label">First Name</label>
    <input v-model="student.first_name" class="form-control" placeholder="First Name" />
  </div>

  <div class="mb-3">
    <label class="form-label">Last Name</label>
    <input v-model="student.last_name" class="form-control" placeholder="Last Name" />
  </div>

  <div class="mb-3">
    <label class="form-label">Student ID</label>
    <input v-model="student.student_id" class="form-control" placeholder="Student ID" />
  </div>

  <div class="mb-3">
    <label class="form-label">Major</label>
    <input v-model="student.major" class="form-control" placeholder="Major" />
  </div>

  <div class="mb-3">
    <label class="form-label">School</label>
    <input v-model="student.school" class="form-control" placeholder="School" />
  </div>

  <button @click="saveEdit" class="btn btn-success w-100">Save</button>
  </div>

  </div>

<footer id="contact">
    <span>Contact</span>
    <div>        
    <p class="contact">Tel: 0938546666</p>
    <p class="contact">Email: ukikillme@gmail.com</p>
    <a class="contact" href="https://www.facebook.com/uki.awirootcheewin/">
            <img id="facebook" width="48" height="48" src="../assets/images/Facebook.png"></a>
    <a class="contact" href="https://www.instagram.com/uki_p11/" >
            <img id="ig" width="48" height="48" src="../assets/images/Instagram.png"></a>
    <a class="contact" href="http://discordapp.com/users/737996018758713456"> 
            <img id="discord" width="48" height="48" src="../assets/images/Discord.png"></a>
    </div>
</footer>

</div>
</template>

<script>
export default {
  name: "MeCard",
  data() {
    return {
      student: {},
      editMode: false,
    };
  },
  methods: {
    async getStudent() {
      const response = await fetch("http://localhost:3000/student");
      this.student = await response.json();
    },
    async updateStudent() {
      await fetch("http://localhost:3000/student", {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.student),
      });
    },
    toggleEdit() {
      this.editMode = !this.editMode;
    },
    async saveEdit() {
      await this.updateStudent();
      this.toggleEdit();
    },
  },
  mounted() {
    this.getStudent();
  },

};

</script>

<style scoped>
#body{
  background-color: lightblue;
}
#body{
  font-family: "Pixelify Sans", sans-serif;
  background-image: url("https://images5.alphacoders.com/118/1183450.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  margin: 0;
  padding: 0;
  color: whitesmoke;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

#edit-block {
  border: black solid 4px;
  color: black;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  text-align: center;
  height: 50%;
  width: 30%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.input-field {
  width: 80%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

.button-group {
  margin-top: 1rem;
  margin-top: 20px;
}

.btn {

  margin: 5px;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
}

 #card{
    margin-right: auto;
    margin-left: auto;
    background-image: url("https://opengameart.org/sites/default/files/5_71.png");
    background-repeat: no-repeat;
    background-size: 100% 100%;
    border: whitesmoke solid 2px;
    border-radius: 10px;
    width: 60%;
    margin-top: 80px;
    margin-bottom: 80px;
    padding-top: 80px;
    padding-bottom:50px;
} 
#card #head{
    padding-bottom:50px;
    display:grid;
    grid-template-columns: 1fr 1fr;
}
#card #head #left{
    width: 300px;
    height: 300px;
    display: block;
    margin-left: auto;
    margin-right: auto;
}
#card #head #left img {
    border: 5px solid whitesmoke;
    width:300px;
    height:300px;
}
#card #head #right{
    background: linear-gradient(black,darkblue,blue,green);
    border: whitesmoke solid 2px;
    text-align: center;
    border-radius: 10px;
    margin-right: 50px;
    p{
        padding-top: 1.5rem;
        color: whitesmoke;
        font-size: 1.5rem;
        font-weight: 500;
    }
}

#card #foot {
    display: flex;
    justify-content: space-between;
    margin-left: 100px;
    margin-right: 100px;
}

#card #foot img {
    width: 24px;
    height: 24px;
}
#card #foot img:hover{
    width: 45px;
    height: 45px;
} 

footer{
    font-size: 1.1rem;
    margin-top: 19rem;
    background-color: rgb(40,40,40);
    text-align: center;
    padding: 20px 0;
}

footer div{
    width: 60%;
    margin: auto;
    display: flex;
    justify-content: space-between;
}

.contact{
    padding: 10px;
    color: white;
    text-decoration: none;
}
</style>