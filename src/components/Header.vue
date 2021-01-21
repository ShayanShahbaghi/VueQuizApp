<template>
  <div class="header shadow">
      <h1 class="category">
          Technology
      </h1>
      <h1 class="qCounter">
          {{ this.questionNumber }} / 10
      </h1>
  </div>
</template>

<script>
export default {
    props: {
        questionNumber: Number
    }
}
</script>

<style>
.category {
    display: inline-block;
    width: 48%;
    text-align: left;
    margin-left: 2%;
}
.qCounter {
    display: inline-block;
    width: 48%;
    float: right;
    text-align: right;
    margin-right: 2%;
}
.shadow {
    box-shadow: 0 .5rem 1rem rgba(0,0,0,.15)!important;
}
.header::after {
    content: '';
    display: table;
    clear: both;
}
</style>