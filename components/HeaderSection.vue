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

      <div>
        <img src="assets/bag.svg" alt="SVG bag" />
      </div>
 

      <div class="profile">
        <div>
          <img src="assets/profile.svg" alt="SVG profile" />
        </div>
      </div>


    </div>
  </div>
</template>

<script>
export default {
  name: "AppHeader"
}
</script>

<style scoped>

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