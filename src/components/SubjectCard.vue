<template id="SubjectCard">
  <div id="body" >
  <!--  show subject -->
  <div>
     <!--  add subject -->
    <div class="card p-3 mb-3">
      <h3>Add New Subject</h3>
      <input class="form-control mb-2" v-model="NewSubject.subject_id" placeholder="Subject ID" required />
      <input  class="form-control mb-2" v-model="NewSubject.name" placeholder="Subject Name" required />

    <select class="form-select mb-2" v-model="NewSubject.grade" required>
    <option disabled value="">Select grade</option>
    <option v-for="grade in ['A','B+','B','C+','C','D+','D','F']" :key="grade" :value="grade">
      {{ grade }}
    </option>
  </select>

  <select class="form-select mb-2" v-model="NewSubject.credit" required >
    <option disabled value="">Select Credit</option>
    <option v-for="credit in [1, 2, 3, 4]" :key="credit" :value="credit">
      {{ credit }}
    </option>
  </select>
      <button class="btn btn-success"  @click="addSubjects()">Save</button>
    </div>

    <!-- show subject -->
    <h3 class="show-data">Subjects</h3>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Grade</th>
          <th>Credit</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in subjects" :key="item.id">
          <td>{{ item.subject_id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.grade }}</td>
          <td>{{ item.credit }}</td>
          <td>
          <a href="#edit"><button class="edit-btn" @click="()=>{
          let key = Object.keys(item)
          key.forEach((v,i)=>{//map new subject (same key)
            editSubject[v]  = item[v]
          })
          openEditBlock = true;
          }">Edit</button></a>
          <button class="bg-danger" @click="deleteSubjects(item.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

    <!--  edit subject -->
    <div v-if="openEditBlock" class="card p-3 mt-3" id="edit">
      <h3>Edit Subject</h3>
      <input  class="form-control mb-2" v-model="editSubject.subject_id" placeholder="Subject ID" required />
      <input class="form-control mb-2" v-model="editSubject.name" placeholder="Subject Name"  required/>
    
  <select class="form-select mb-2" v-model="editSubject.grade" required >
    <option disabled value="">Select GPA</option>
    <option v-for="grade in ['A','B+','B','C+','C','D+','D','F']" :key="grade" :value="grade">
      {{ grade }}
    </option>
  </select>

  <select  class="form-select mb-2" v-model="editSubject.credit" required >
    <option disabled value="">Select Credit</option>
    <option v-for="credit in [1, 2, 3, 4]" :key="credit" :value="credit">
      {{ credit }}
    </option>
  </select>

      <button  class="btn btn-success me-2"  @click="updateSubjects()">Save</button>
      <button class="btn btn-secondary"  @click="()=>{ openEditBlock = false; editSubject={};}">Close</button>
    </div>
</div>
</template>
  
<script>
import { v4 as uuidv4 } from "uuid";

export default {
name:"SubjectCard",//name commponent
data() {
  return {
    NewSubject: {      
      "subject_id": "",
      "name": "",
      "grade": "",
      "credit": 0
    },
    editSubject:{},
    subjects: [],
    openEditBlock:false,
  };
},

methods: {
  async getSubjects() {
    const response = await fetch('http://localhost:3000/subjects');
    this.subjects = await response.json();
},
  async addSubjects(){
    let flat = false
    let key = Object.keys(this.NewSubject)
          key.forEach((v,i)=>{//map new subject (same key)
            if (this.NewSubject[v] === "" || this.NewSubject.credit === 0){
              flat = true
              return // what the fuck why return don't work fuck you javascritp
            }
          })
    if (flat){return}
    this.NewSubject.id = uuidv4()
    await fetch('http://localhost:3000/subjects',{
      method:"POST",
      headers: {'Content-Type': 'application/json',},
      body:JSON.stringify(this.NewSubject)
    });
    this.NewSubject={      
      "subject_id": "",
      "name": "",
      "grade": "",
      "credit": 0
    }
    this.getSubjects()
  },
  async updateSubjects(){
        await fetch(`http://localhost:3000/subjects/${this.editSubject.id}`,{
            method:"PUT",
            headers: {'Content-Type': 'application/json',},
            body:JSON.stringify(this.editSubject)
            })
    this.getSubjects()
    this.editSubject= {}
    this.openEditBlock = false
    },
  async deleteSubjects(id){
    await fetch(`http://localhost:3000/subjects/${id}`,{
      method:"DELETE"
    })
    this.getSubjects()
  }
},

mounted() {
  this.getSubjects();
},

}
</script>

<style scoped>
#body{
  background-color: lightblue;
}
#body{
  font-family:Arial, sans-serif;
  background-image: url("../assets/images/wallpaperflare.com_wallpaper.jpg");
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
.Card{
  font-family: 'Courier New', Courier, monospace;
}

.card {
  margin: auto;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  background-color: #f9f9f9;
  margin-top: 4rem;
  width: 70%;
}

.show-data{
  color: black;
  margin-top: 4rem;
  text-align: center;
}

table {
  color: black;
  margin: auto;
  width: 70%;
  border-collapse: collapse;
  margin-top: 10px;
  background-color: lightblue;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  overflow: hidden;
}

th, td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: left;
}

th {
  background-color: #4CAF50;
  color: white;
}

tr:hover {
  background-color: #ddd;
}

button {
  padding: 6px 12px;
  margin: 2px;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}

.edit-btn {
  margin-left: 1rem;
  background-color: #ffc107;
  color: black;
}

.bg-danger {
  margin-left: 1rem;
  background-color: #f44336;
}

.edit-btn:hover {
  background-color: #e0a800;
}

.bg-danger:hover {
  background-color: #d32f2f;
}

.edit-form {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.edit-form label {
  display: block;
  margin: 10px 0;
}

.save-btn {
  background-color: #4CAF50;
  color: white;
}

.cancel-btn {
  background-color: #757575;
  color: white;
}

.save-btn:hover {
  background-color: #45a049;
}

.cancel-btn:hover {
  background-color: #616161;
}
</style>