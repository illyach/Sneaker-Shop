<script setup>
const inputCategory = ["Home", "New Arrivals", "Sale", "Clothing"]

const { data } =  useFetch( () => '/api/sneakers' );

const main = reactive({
      selectedImage: '/teal_joyride.png',
      selectedImageIndex: null,
      selectedImageColor: '#FFA500', 
      selectedImageArray: [],
      selectedColorImage: '',
      selectedSneakerName: 'JOYRIDE',
      selectedSneakerNameFirstWord: '',
      selectedSneakerNameSecondWord: '',
      colorsCode: [],
      arrImages:['/blu_fly_by_mid.png', '/orange_fly_by_mid.png', '/white_fly_by_mid.png'],
      title: 'ABSORBS THE IMPACT',
      titleTwo: 'Feels Fresh Every Run',
      description: 'That soft ride doesn’t just go easy on your feet—it helps your whole body feel good.',
      descriptionTwo: 'Designed to work for every runner, at every stage of their journey.',
      date: 'JANUARY 6, 2023',
      sneakerName: 'NIKE JOYRIDE',
      sneakerPrice: 0
})


const button = reactive({
  right: false,
  left: false,
  addToBag: false,
  viewDetails: false,
  addToBagProps: false
})


const buttonPressed = ref(false)


let borderObject = '0 0 0 4px white, 0 0 0 6px #DADADA';

let currentIndex = 0

function rightButtonAnimation(){
  button.right = true 
  
  setTimeout(() => {
      button.right = false
  }, 180)
}

function leftButtonAnimation(){
  button.left = true

  setTimeout(() => {
    button.left = false
  }, 180)
}

function buttonViewDetailsClicked(){
  button.viewDetails = true
  setTimeout(() => {
    button.viewDetails = false
  }, 180)
}

function buttonAddToBagClicked(){
  button.addToBag = true
  setTimeout(() => {
    button.addToBag = false
  }, 180)
}

function nextImage(){
  borderObject = 'none'
  buttonPressed.value = true
  let findPrice = main.selectedImageArray.find((i) => i.image === main.selectedImage)?.price
  console.log(findPrice)

  setTimeout(() => {
    buttonPressed.value = false
}, 180);

currentIndex = (currentIndex + 1) % (main.arrImages.length);

main.selectedImage = main.arrImages[currentIndex]
}


function findColorImage(colorCode, arr){
  borderObject = '0 0 0 4px white, 0 0 0 6px #DADADA';

  let findColorImageCode = arr.find((i) => i.code === colorCode).code
  let findColorCodeImage = arr.find((i) => i.code === colorCode).image
  let findPriceByColor = arr.find((i) => i.code === colorCode).price;
  main.selectedColorImage = findColorImageCode
  main.selectedImage = findColorCodeImage
  main.price = findPriceByColor
  console.log(main.price)
}


function findImage(image, index, arr, color, sneaker_name, title, description, title_two, description_two, date, price ) {
  borderObject = 'none'
  main.selectedImage = image;
  main.selectedImageIndex = index
  main.selectedImageColor = color
  main.selectedImageArray = arr
  main.selectedSneakerName = sneaker_name.replace("NIKE ", "").replace(" ", "");
  main.colorsCode = arr.map((i) => i.code)
  main.arrImages = arr.map((i) => i.image)
  main.title = title
  main.titleTwo = title_two
  main.description = description
  main.descriptionTwo = description_two
  main.sneakerName = sneaker_name
  main.date = date
  main.sneakerPrice = price
  console.log(main.sneakerPrice)


}



</script>

<template>


<header-section :props="button.addToBagProps ? { name: main.sneakerName, image: main.selectedImage, price: main.sneakerPrice } : null" />
<header-nav/>


<!--  Left side of the page-->
    <div class="content">
      <div class="wrapper">
        <div class="header">
            <div class="date">
                    <ul>
                        <li>realse date</li>
                        <li>{{main.date}}</li>
                        <li>limited stocks only</li>
                    </ul>
            </div>



              <div :class="{ pressAnimation: button.left }">
                <div class="left_arrow" >

                <div @click="nextImage(currentIndex), leftButtonAnimation()">
                  <img  src="assets/arrow.svg" alt="SVG search" />
                </div>
              </div>
              </div>
            


            <div class="description_left">
                <p>{{main.title}}</p>
                <p>{{main.description}}</p>
            </div>
          <!--      Left side of the page -->



            <!-- Centered elements | sneaker model NAME & sneaker IMAGE -->
          <div class="name" >
            <img class="right_grapes" src="/grapes.png">
            <p class="nike">&nbsp;NIKE</p>
            <p class="joyride" :style="{ 'padding-left': main.selectedSneakerName === 'JOYRIDE' || (main.selectedSneakerName.charAt(0) === 'A') ? '200px' : '0px' }">
              {{main.selectedSneakerName}}
            </p>

          <Transition name="animate" >

              <div class="my_img"  v-if="buttonPressed" :style="'display:none'">
                <div>
                  <img :src="main.selectedImage" :key="main.selectedImage">
                </div>
              </div>

              <div class="my_img" v-else>
                <div>
                  <img :src="main.selectedImage" :key="main.selectedImage" >
                </div>
              </div>

          </Transition>


            <img class="left_grapes" src="/grapes.png">
        </div>
        <!-- Centered elements | name & image  -->



    <!--Right side of the page-->

          <div class="r"/>
         <div class="description_right">
                      <p>{{main.titleTwo.toUpperCase()}}</p>
                      <p>{{main.descriptionTwo}}</p>
          </div>

          <div :class="{ pressAnimation: button.right }">
              <div class="right_arrow">
                <div @click="nextImage(currentIndex), rightButtonAnimation()">
                  <img  src="assets/arrow.svg" alt="SVG search" />
                </div>
              </div>
        </div>

          <div class="colors">
            <div class="wrapper_colors">
              <p>new arrival</p>
              <p>{{main.sneakerName}}</p>


                <div class="colors3">

                  <div v-for="(color, colorIndex) in main.colorsCode" :key="colorIndex" class="colors_container"    >
                    <div @click="findColorImage(color, main.selectedImageArray)" class="rounded" :style="{ 'backgroundColor': color, 'box-shadow': color === main.selectedColorImage ? borderObject : 'none' }"></div>
                  </div>

              </div>
            </div>
          </div>
          <!--Right side of the page-->
        </div>
      </div>
    </div>



    <div class="buttons">
      <div class="buttons_wrapper">
        <button :style="{transform: button.addToBag ? 'scale(0.97)' : 'scale(1)'}" @click="buttonAddToBagClicked(), button.addToBagProps = true">+ Add to Bag</button>
        <button :style="{transform: button.viewDetails ? 'scale(0.97)' : 'scale(1)'}" @click="buttonViewDetailsClicked()">View Details →</button>
      </div>
    </div>

    




    <div class="items_text">
        <p>NEW ARRIVALS COLLECTION</p>
    </div>

<!-- sneakers -->
    <div v-for="(item, index) in data" :key="item.code">
        <div class="sneakers">
          <div v-for="(color, colorIndex) in item.colors" :key="color.code" class="sneaker" :style="{ border: color.image === main.selectedImage ? '4px solid #5CE1E6' : 'none' }">
              <img :src="color.image"  @click="findImage(color.image, colorIndex, item.colors, color.code, data.find((i) => i.colors.some((e) => e.image === color.image)).name, item.title, item.description, item.title_two, item.description_two, item.date, color.price)">
          </div>
        </div>
      </div>


  </template>

  <style scoped>
  body {
    background-color: #f0f0f0;
  }
  .pressAnimation {
    animation: press 0.2s 1 linear;
  }
  
  @keyframes press {
    0% {
      transform: scale(1);
    }
    50% {
      transform: scale(0.94);
    }
    to {
      transform: scale(1);
    }
  }

  .border_visible{
    border:0.14rem solid black;
    border-radius: 50%;
  }

  .animate-enter-active,
  .animate-leave-active {
    transition: opacity 0.5s ease;
  }

  .animate-enter-from,
  .animate-leave-to {
    opacity: 0;
  }

   




    /* ARROW SVG */
.left_arrow{
   display: flex;
   padding-left: 30px;
}

.right_arrow{
    transform:scale(-1,1);

}


    /* ARROW SVG  END */

/* right description and left description */

  .description_left{
    padding-left: 30px;
  }

 .description_right{
    padding-left: 30px;
 }

.description_right  :nth-child(1){
  font-family: Roboto, sans-serif;
  font-size: 19px;
  font-weight: 900;
  line-height: 3px;
  letter-spacing: 0em;
  text-align: left;
}


  .description_right :nth-child(2){
    font-family: Roboto Thin, sans-serif;
  font-size: 19px;
  font-weight: 200;
  line-height: 25px;
  letter-spacing: 0em;
  text-align: left;
  color: #7E7E7E;
  }

  .description_left  :nth-child(1){
  font-family: Roboto, sans-serif;
  font-size: 19px;
  font-weight: 900;
  letter-spacing: 0em;
  text-align: left;
  }

  .description_left :nth-child(2){
  font-family: Roboto Thin, sans-serif;
  font-size: 19px;
  font-weight: 200;
  line-height: 25px;
  letter-spacing: 0em;
  text-align: left;
  color: #7E7E7E;
  }
  /* description end*/



  .items_text{
    display: flex;
    justify-content: center;
    color:#5CE1E6;
    margin-top: 73px;
    font-family: Roboto, sans-serif;
    font-size: 24px;
    font-weight: 700;
    line-height: 29px;
    letter-spacing: 0.3px;
    text-align: left;

  }



  /* colors rounded | select sneaker color */

    .colors3 {
    display: flex;
    flex-direction: row;
    gap:15px;
    }


    .colors p:nth-child(2){
      font-family: Roboto, sans-serif;
      text-transform: uppercase;
      font-size: 25px;
      letter-spacing: 0em;

      transform: skew( -0.152rad);
    }

    .colors p:nth-child(1){
    color: #5CE1E6;
    font-family: Roboto, sans-serif;
    text-transform: uppercase;
    font-size: 20px;
    font-weight: 700;
    letter-spacing: 0em;

    }

.colors_container{
  border-radius: 50%;

}
    .rounded{
      width: 34px;
      height: 34px;
      border-radius: 50%;
    }
    /*  colors rounded | select sneaker color */


    /*list of sneakers section*/
  .sneaker img{
    transform: rotate(34deg) scale(-1, 1);
    width: 180px;
    margin: 4px;
    height: 160px;
    margin-top: 22px;
    margin-left: 38px;
    border-radius: 30px;
  }

    .sneaker {

      flex: 0 1 calc(17% - 10px);
      width: 200px;
      height: 160px;
      margin: 4px;
      background-color: #ededed;
      border-radius: 30px;
      box-sizing: border-box;
    }

  .sneakers{

    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 20px;
    max-width: 1500px;
    margin: 5px auto;


  }
/*list of sneakers section*/



/* Add bag , View details  BUTTONS*/
  .buttons{
    display: flex;
    justify-content:center;
    margin-top:30px;
    padding: 30px;
    border-radius: 10px;
    transform: scale(1.5);
}
  .buttons_wrapper > button{
    width: 130px;
    height: 34px;
    border-radius: 20px;
    margin-left: 30px;
    background-color: #FFFFFF;
  }

    .buttons_wrapper :nth-child(1){
      font-family: Roboto, sans-serif;
      color: #FFFFFF;
      background-color:#1E1E1E;
      border: 2px solid #0a0a0a;
    }

    .buttons_wrapper :nth-child(2){
      font-family: Roboto, sans-serif;
     background-color: #FFFFFF;
      color: #919090;
      border: 2px solid #EFEFEF;
    }
/* Add bag , View details  BUTTONS*/

  .content {
    display: flex;
    justify-content: center;
  }

  .header {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    flex-direction: column;
    margin-top:50px;
    width: 1500px;
    height: 800px;

    align-content: space-between
  }

  .header > div:not(.name):not(.image):not(.r) {
    width: 270px;
    height: 130px;
    margin: 10px;
  }

  .nike{
    position: absolute;
    margin: -290px;
    padding-top: 90px;
    width: 10px;
    height: 10px;
    margin-top: 100px;
    z-index: -1;
    width: 267px;
    height: 90px;

    font-family: Roboto, sans-serif;
    font-size: 148px;
    font-style: italic;
    font-weight: 900;
    line-height: 158px;
    letter-spacing: 0em;
    text-align: left;
    color:#F1F1F1;
}
.nike_name{
margin-left: 15px;
}
.joyride{
  white-space: nowrap;

    position: absolute;
    padding-top:300px;

   width: 10px;
   height: 10px;
    z-index: -1;
    width: 230px;
    height: 70px;
    margin-top:30px;
    font-family: Roboto, sans-serif;
    font-size: 148px;
    font-style: italic;
    font-weight: 600;
    line-height: 158px;
    letter-spacing: 0em;
    text-align: left;
    color:#F1F1F1;
}


.my_img{
    margin-top: 90px;
}

.left_grapes{
position: absolute;
}

.right_grapes{
    position: absolute;
    margin-left: 500px;
    margin-top: 70px;
}


  .date ul li:nth-child(3){
    color: #7E7E7E;
    font-family: Roboto, sans-serif;
    font-size: 18px;
    font-weight: 850;
    line-height: 28px;
    letter-spacing: 0em;
    text-align: left;


    }

    /* realse date section  */
    .date ul li:nth-child(2){
    font-family: Roboto, sans-serif;
    font-size: 23px;
    font-weight: 750;
    line-height: 38px;
    letter-spacing: 0em;
    text-align: left;
    transform: skew( -0.152rad);

    }

    .date ul li:nth-child(1){
      color: #5CE1E6;
      font-family: Roboto, sans-serif;
    font-size: 18px;
    font-weight: 750;
    line-height: 28px;
    letter-spacing: 0em;
    text-align: left;


    }

    .date ul{
      text-transform: uppercase;
      list-style-type: none;
      font-family: Roboto, sans-serif;
    }

    .date{
    width: 270px;
    height: 71px;
    top: 233px;
    left: 120px;
    gap: 16px;
    }
      /* realse date section */

    /*occupies an invisible space so that the order of the flex elements is preserved*/
  .r{
    background-color: white;
width: 200px;
height: 150px;
align-self: center;
 visibility: hidden;
  }

  </style>
  