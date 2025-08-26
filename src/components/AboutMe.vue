<template>
    <div id ="body">
    <div id="about_me">
        <p>about me</p>
        <div class="imgs">
        <img src="your image" width="300" height="300">
        <img src="your image" width="300" height="300">
        </div>
    </div>

    <section id="education">
        <h2>Education</h2>
        <ul>
        </ul>
    </section>
    
    <section id="present">
        <h2>History</h2>
        <p>
        </p>
    </section>
    
</div>
</template>

<script>

export default  {
name: "AboutMe"
}
</script>

<style scoped>
#body{
  background-color: lightblue;
}
#body{
  font-family: "Pixelify Sans", sans-serif;
  background-image: url(https://wallpapers.com/images/featured/8-bit-background-00eolrvv0ccowrjf.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  margin: 0 ;
  padding: 0;
  color: whitesmoke;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
#about_me {
    background: linear-gradient(black,darkblue,blue,green);
    border: whitesmoke solid 2px;
    border-radius:10px;
    padding:1rem;
    width:40%;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    margin:1rem auto;
}
#about_me p {
    font-size:2rem;
    color:whitesmoke;
    margin:0 0 10px;

}
.imgs {
    display: flex;
    justify-content: center; /* Centers images horizontally */
    gap: 2rem; /* Adds spacing between images */
    margin: 0 auto;
}

p{
    color: whitesmoke;
}
li{
    color: whitesmoke;
}
#about_me img {
    border-radius: 10px;
}

section {
    padding: 2rem;
    margin: 2rem auto;
    width: 50%;
    background: linear-gradient(black ,blue);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    border: whitesmoke solid 2px;
    border-radius: 10px;
}

h2 {
    color: #4CAF50;
}

ul {
    list-style-type: none;
    padding: 0;
}

ul li {
    padding: 0.5rem 0;
}

</style>