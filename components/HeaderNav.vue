<script setup>
const inputCategory = ["Home", "New Arrivals", "Sale", "Clothing"]

</script>

<template>

        <div class="input_container">
            <div class="input_wrapper">
                    <div v-for="element in inputCategory" :key="element" class="input_element">
                        <input
                          name="category"
                          :id="element"
                          type="radio"
                        />
                        <label :for="element">{{ element }}</label>
                </div>
            </div>
        </div>

</template>


<style  scoped>
  /* Navigation inputs Start */
  .input_container {
    display: flex;
    justify-content: center;
    align-content: center;
    margin: 0 auto;
    border-radius: 25px;
    padding: 5px;
    background-color: #ffffff;
    height: 56px;
    width: max-content;
    margin-bottom: 60px;
    box-shadow: 0px 4px 20px 0px #8E8E8E1A;
  }

  .input_wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .input_element input {
    display: none;
  }

  .input_element {
    margin-left: 40px;
    margin-right: 40px;
  }

  .input_element label {
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 600;
    font-family: Roboto, sans-serif;
    font-size: 18px;
    line-height: 24px;
    color: #7E7E7E;
    padding: 0 22px;
    border-radius: 8px;
    cursor: pointer;
    height: 40px;
  }

  .input_element input:checked ~ label {
    background: #1E1E1E;
    border-radius: 30px;
    color: #ebe9fe;

  }

  /* NAvigation inputs End */
</style>