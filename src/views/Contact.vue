<template>
  <div class="contact-info">
    <div class="contact-method">
      <i class="fas fa-envelope"></i>
      <span>p.greber2504@gmail.com</span>
    </div>

    <div class="contact-method">
      <i class="fab fa-github"></i>
      <span>github.com/pgreber2504</span>
    </div>

    <div class="contact-method">
      <i class="fab fa-linkedin"></i>
      <span>linkedin.com/in/pgreber2504/</span>
    </div>

    <div class="contact-method">
      <i class="fas fa-map-marker-alt"></i>
      <span>Lodz, PL</span>
    </div>
  </div>
</template>

<style lang="scss">
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.12.0-2/css/all.min.css");

.contact-info {
  position: absolute;
  width: 100%;
  top: 55%;
  transform: translateY(-50%);
  text-align: center;
}

.contact-method {
  width: 220px;
  height: 140px;
  display: inline-block;
  background-color: #f9feff;
  margin: 10px;
  position: relative;
  color: #485e74;
  cursor: pointer;
}

@media (max-height: 700px) {
  .contact-info {
    top: 70%;
  }
}

.contact-method i {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  font-size: 30px;
  line-height: 140px;
  background-color: #7396b8;
  transition: transform 0.6s;
  z-index: 1;
}

.contact-method span {
  position: absolute;
  width: 100%;
  left: 0;
  bottom: 0;
  padding: 10px 0;
}

.contact-method i:hover {
  transform: translateY(-40%);
}
</style>