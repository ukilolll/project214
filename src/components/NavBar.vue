<template>
    <header>
    <span id="text"></span>
    <nav>
    <a href="#" @click.prevent="$emit('navigate', 'MeCard')">Home</a>
    <a href="#" @click.prevent="$emit('navigate', 'AboutMe')">About Me</a>
    <a href="#" @click.prevent="$emit('navigate', 'SubjectCard')">My subject</a>
    </nav>
    </header>
</template>

<script>
export default {
name:"NavBar"

}

</script>

<style>

header {
    font-family: "Pixelify Sans", sans-serif;
    color: black;
    background: linear-gradient(green,lime,rgb(76, 221, 224),rgb(119, 201, 228));
    padding: 1rem 0;
    text-align:center;
    display: grid;
    grid-template-columns: 1fr 1fr;
    font-weight: 800;
    font-size: 2rem;
    padding-bottom: 40px;
    position: relative;
    padding-top: 2.5rem;
}
header #text{
    position: absolute;
    left: 20%;
    animation: abomination1 5s linear 1;
    animation-fill-mode: forwards;
    width: 200px;
    
}
header #text:after {
    position: absolute;
    content: "";
    width: 100%;
    height: 100%;
    line-height: 48px;
    left: 30%;
    top: 50%;
    animation: abomination1 5s linear infinite;
    animation-fill-mode:forwards;
  }
header nav{

    position:absolute;
    right: 10%;
}
@keyframes abomination1 {
    10%{
        content:"M";
    }
    20%{
        content:"My";
    }
    30%{
        content:"My ";
    }
    40%{
        content:"My P";
    }
    50%{
        content:"My Pr";
    }
    60%{
        content:"My Pro";
    }
    70%{
        content:"My Prof";
    }
    80%{
        content:"My Profi";
    }
    90%{
        content:"My Profil";
    }
    100%{
        content:"My Profile";
    }
}
header nav{
    display: inline-block;
    justify-content: space-between;
    text-align:center;
    /* right: 30%;  */
}
header nav a {
    font-size: 1.5rem;
    color: black;
    text-decoration: none;
    margin-left: 20px;
    margin-right: 20px;
}
header nav a:hover{
    color: white;
}
</style>