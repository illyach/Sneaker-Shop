<template>
  <div class="elements">

      <div class="seacrh-svg">
        <SearchSvg/>
      </div>

    <div class="logo-svg">
      <LogoSvg/>
    </div>

    <div class="bag-svg">
       <BagSvg/>
      <div class="profile">
        <ProfileSvg/>
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