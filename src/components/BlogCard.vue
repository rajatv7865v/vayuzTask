<template>
    <div class="Card-container">
        <div class="img-container"><img v-bind:src= item.image   alt="logo"></div>
        <div class="name-Cont">
            <h3>{{ item.name }}</h3>
        </div>
        <div class="para-Cont">
            <p>{{ item.bio }}</p>
        </div>
    </div>
</template>

<script>
export default{
    name:'BlogCard',
    props:{
        item:Object
    }
}
</script>
<style scoped>
*{
    margin: 0;
    padding: 0;
}
.Card-container{
width: 16vw;
height: 30vh;
border: 1px solid grey;
margin: 20px;
}
.img-container{
margin: 5px;
}
.img-container img{
width: 150px;
}
.name-Cont{
font-size: 15px;
padding: 8px;
}
.para-Cont{

}

</style>
