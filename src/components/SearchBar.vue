<template>
  <div class="container search-box">
    <div class="input-group mb-3">
      <input type="text" class="form-control" v-model="inputValue" @keypress.enter="onTextSearch" placeholder="Search for a city. . ." aria-label="Search for a city. . ." aria-describedby="button-addon2">
      <div class="input-group-append">
        <button class="btn btn-outline-info" type="button" id="button-addon2" @click="onTextSearch"><strong>Search</strong></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      inputValue: null
    }
  },
  methods: {
    onTextSearch(){
      try {
        this.$emit('citySearch', this.inputValue)
      }catch(err){
        throw err
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  margin: 0 20px;
  border-radius: 10px 10px;
}

</style>
