<template>
  <div class="item">
    <p class="header">
      <slot name="header"></slot>
    </p>
    <p class="details">
        <slot name="notes"></slot>
    </p>
  </div>
</template>

<style scoped>
.item {
  margin-top: 5rem;
  display: flex;
  flex-direction: column;
  text-align: center;
}

.details {
  flex: 1;
  margin-left: 1rem;
  font-size: 1.8rem;
  font-weight: normal;
}

.header{
    font-size: 3.5rem;
    text-align: center;
    font-weight: bold;

    background: linear-gradient(
      to right, 
      hsl(98 100% 62%), 
      hsl(204 100% 59%)
    );
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    text-align: center;
}

</style>
