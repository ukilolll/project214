<template>
  <NavBar @navigate="changeComponent" />
  <component :is="currentComponent" />
</template> 

<script>
  import MeCard from './components/MeCard.vue';
  import SubjectCard from './components/SubjectCard.vue';
  import NavBar from './components/NavBar.vue';
  import AboutMe from './components/AboutMe.vue';
  export default {
    components:{
      MeCard,
      SubjectCard,
      NavBar,
      AboutMe
    },

    data() {
    return {
      currentComponent: "MeCard",
    };
  },

  methods: {
    changeComponent(componentName) {
      this.currentComponent = componentName;
    },
  }

  }
</script>