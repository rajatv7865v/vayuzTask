<template>

    <div>
        <input type="text" v-model="formData.name" placeholder="Enter Name">
        <input type="text" v-model="formData.bio"  placeholder="Enter Bio">
        <input type="text" v-model="formData.image"  name="" id="" placeholder="Image link">
        <button v-on:click="addCard">Add Card</button>
    </div>
    <div>
        <button v-on:click="deleteData">Delete Last Card</button>
    </div>
  <div class="Home-container">
    <div  v-for="item in cardData" :key="item.name">
    <BlogCard v-bind:item="item" />
  </div>
  </div>
</template>
<script>
import BlogCard from "./BlogCard.vue";

export default {
  name: "HomePage",
  components: {
    BlogCard,
  },
  methods:{
    addCard(){
//   console.log("add card ",this.formData.cardName)
    this.cardData=[...this.cardData,this.formData] 
    },
    deleteData(){
       this.cardData= this.cardData.filter((item,i)=>i!=this.cardData.length-1)
    //    console.log("delete")
    }
  },
  data() {
    return {
        formData:{
          image:null,
          name:null,
          bio:null,
        },
        
      cardData: [
        {
          image:
            "https://images.unsplash.com/photo-1587474260584-136574528ed5?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8ZGVsaGl8ZW58MHx8MHx8&w=1000&q=80",
          name: "India Gate",
          bio: "It is situated in Delhi.",
        },
        {
          image:
            "data:image/jpeg;base64,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",
          name: "Nature",
          bio: "This image is shoot in evening time.",
        },
        {
          image:
            "data:image/jpeg;base64,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",
          name: "Eye Image",
          bio: " eye Image.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQdxpKUACkSklSrDrDlc37bwXy-98HkB_vyjg&usqp=CAU",
          name: "Google logo",
          bio: "This logo is google photos.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRNaI3k3GEVnCEXd54ISam3Ix7uwWZtIj1nHg&usqp=CAU",
          name: "Independence Day",
          bio: "Independence day.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQkTQ8DFOgujidIRil33r2QnSZ2Y_ZHahrUlw&usqp=CAU",
          name: "Ratina",
          bio: "Eye Ratina",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRNaI3k3GEVnCEXd54ISam3Ix7uwWZtIj1nHg&usqp=CAU",
          name: "Independence Day",
          bio: "Independence day.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRNaI3k3GEVnCEXd54ISam3Ix7uwWZtIj1nHg&usqp=CAU",
          name: "Independence Day",
          bio: "Independence day.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRNaI3k3GEVnCEXd54ISam3Ix7uwWZtIj1nHg&usqp=CAU",
          name: "Independence Day",
          bio: "Independence day.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRrTFrhr_-pYR74jUgOy7IerAoHAX3zPIZZcg&usqp=CAU",
          name: "Tiger",
          bio: "Tiger Image.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRrTFrhr_-pYR74jUgOy7IerAoHAX3zPIZZcg&usqp=CAU",
          name: "Tiger",
          bio: "Tiger Image.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRrTFrhr_-pYR74jUgOy7IerAoHAX3zPIZZcg&usqp=CAU",
          name: "Tiger",
          bio: "Tiger Image.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRrTFrhr_-pYR74jUgOy7IerAoHAX3zPIZZcg&usqp=CAU",
          name: "Tiger",
          bio: "Tiger Image.",
        },
        {
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRrTFrhr_-pYR74jUgOy7IerAoHAX3zPIZZcg&usqp=CAU",
          name: "Tiger",
          bio: "Tiger Image.",
        },
      ],
    };
  },
};
</script>
<style scoped>
.Home-container {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}
</style>
