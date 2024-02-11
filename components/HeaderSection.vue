<script setup>
const open = ref(false)
defineProps(['props'])
</script>

<template>
  <div class="elements">

      <div class="seacrh-svg">
        <div>
          <img src="assets/search.svg" alt="SVG search" />
        </div>
      </div>

    <div class="logo-svg">
      <div>
        <img src="assets/logo.svg" alt="SVG logo" />
      </div>
    </div>

    <div class="bag-svg">

      <div @click="open = true">
        <img src="assets/bag.svg" alt="SVG bag" />
      </div>


      <Teleport to="body">
        <div v-if="open" class="modal">
          <div class="basket" v-if="props?.image">
            <div>
              <p>Description</p>
              <img :src=props?.image alt="" class="sneaker_img" v-if="props?.image">
              <h1 v-if="props?.name">{{props?.name === undefined  ? 'empty' : props.name}}</h1>
            </div>

            <div>
              <p>Price</p>
            </div>

            <div>
              <p>Size</p>
            </div>

            <div>
              <p>Quantity</p>
            </div>

            <div>
              <p>Total</p>
            </div>

            
          

          </div>
          <div class="close" @click="open = false" >
            <img src="../assets/close.svg" alt="">
          </div>
          <!-- <div class="close">
            <img src="../assets/close.svg" alt="">
          </div> -->

          <div class="empty" v-if="props?.name === undefined">
           <h1>CART</h1>
           <img src="assets/empty.svg"/>
           <h1>IS EMPTY</h1>
           <img src="assets/smile.svg"/>
           </div>
         
        </div>
      </Teleport>

      <div class="profile">
        <div>
          <img src="assets/profile.svg" alt="SVG profile" />
        </div>
      </div>


    </div>
  </div>
</template>



<style scoped>
.empty :nth-child(3){
  margin-left: 18px;
}

.empty :nth-child(4){
  width: 80px;
}
.empty h1{
  display: flex;
  align-items: center;
  font-size: 58px;
  font-family:Arial, Helvetica, sans-serif;
  letter-spacing: 10px;
  }
.empty{
display: flex;
justify-content: center;
}
.empty img{
  width: 150px;
}
.close img{
  width: 60px;
}
.close{
display: flex;
justify-content: center;


max-height: 60px ;
z-index: -1;
margin-left: 1000px;
margin-bottom: 90px;
}

.sneaker_img{
  transform: rotate(-28deg) scale(1, 1);
  width: 100px;
  margin: 4px;
  height: 80px;
}
h1{
  font-size: 20px;
}
.basket{
  font-size: 23px;
  font-family: Arial, Helvetica, sans-serif;
  display: flex;
  justify-content: space-around;
  max-width: 1000px ;
  max-height: 70px ;
}
.modal {
  margin: 0;
  position: fixed;
  top:0;
  left:0;
  border-bottom: 2px solid #ccc;
  margin-bottom: 20%;
  border-radius: 0 0 50% 50%;
  background-color: white;
  width: 100%;
  height: 30%;
  z-index: 999;

}

.profile{
width:70px;
height:70px;
}

.elements{
  display: flex;
  padding: 30px 30px 30px 30px;
  justify-content: space-around;
  gap:20px;
}
.logo-svg{
  display: flex;

}
.bag-svg{
  display: flex;
}

.logo-svg{
  margin-left:34%;
  margin-right:30%;
}
</style>