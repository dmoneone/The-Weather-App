<template>
    <div class="lds-hourglass"></div>
</template>
<style>
  .lds-hourglass {
  display: block;
  margin: 0 auto;
  position: relative;
  width: 64px;
  height: 64px;
}
.lds-hourglass:after {
  content: " ";
  display: block;
  border-radius: 50%;
  width: 0;
  height: 0;
  margin: 6px;
  box-sizing: border-box;
  border: 26px solid #dfc;
  border-color: #dfc transparent #dfc transparent;
  animation: lds-hourglass 1.2s infinite;
}
@keyframes lds-hourglass {
  0% {
    transform: rotate(0);
    animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
  }
  50% {
    transform: rotate(900deg);
    animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
  }
  100% {
    transform: rotate(1800deg);
  }
}

</style>
