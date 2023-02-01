<template>
  <div class="btn">
    
    <h1>Choose the type of question</h1>
    <button @click="$emit('changeOperator', '-')">Subtraction <br />-</button>
    <button @click="$emit('changeOperator', '+')">
      Addition <br />
      +
    </button>
    <button @click="$emit('changeOperator', '*')">
      Multiplication <br />
      X
    </button>
    <button @click="$emit('changeOperator', '/')">
      Division <br />
      ÷
    </button>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
