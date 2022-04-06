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
  margin-top: 4rem;
  display: flex;
  flex-direction: column;
  text-align: center;
  height: 80vh;
  background-image: 
	linear-gradient( rgba(255, 255, 255, 0.8),rgba(179, 255, 131, 0.8));
	  background-size: cover;
  	background-position: top;
  	position: relative;

  	clip-path: polygon(0 0, 100% 0, 100% 58vh, 0 100%);
}

.details {
  flex: 1;
  margin-left: 1rem;
  font-size: 1.8rem;
  font-weight: normal;
}

.header{
    margin-top: 6rem;
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
}
</style>
