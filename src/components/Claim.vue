<template>
  <div class="claimwrapper">
    <p  class="subclaim">PER ASPERA</p>
    <h1 class="claim">AD ASTRA</h1>
    <p class="subclaim">
      Begin your journey through our amazing galaxy <br>
      and discover places you never heard of, with NASA.
    </p>
    <p class="subclaim">
      Type anything space-related to start:
    </p>
  </div>
</template>
<script>
export default {
  name: 'Claim',
};
</script>
<style lang="scss" scoped>
.claimwrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: white;
}

.claim {
  font-size: 50px;
  margin: 0;

  @media (min-width: 768px) {
    font-size: 80px;
  }

  @media (min-width: 1024px) {
    font-size: 100px;
  }
}

.subclaim {
  margin-top: 20px;

  font-size: 13px;
  font-weight: 400;

  @media (min-width: 768px) {
    font-size: 17px;
    line-height: 1;
    letter-spacing: 1px;
    width: 500px;
  }

  @media (min-width: 1024px) {
    font-size: 20px;
  }
}
</style>
