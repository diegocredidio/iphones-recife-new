<template>
  <section class="container">
    <app-logo />
    <section class="container-links">
      <p class="sub" style="font-size: 1.5rem">Quer saber o valor no cartão?</p>
      <nuxt-link v-if="true" to="/simulador" class="button button-large is-link is-medium">
        <span class="icon">
          <img src="~/assets/images/card.png" />
        </span>
        <span><strong>Clique aqui</strong> para Simular</span>
      </nuxt-link>
      <p style="border-bottom: 1px solid black">&nbsp;</p>
      <p class="sub">Clique e Fale Conosco</p>
      <p>Seg a Sex 9h às 18h e Sábado das 9h às 13h</p>


      <a href="https://wa.me/558198788602" class="button btn-column">
        <div class="btn-firstline">
          <span class="icon">
            <img src="~/assets/images/wa.png" />
          </span>
          <span> <b>99878.8602</b> - Daniele </span>
        </div>
      </a>

      <a href="https://wa.me/5581971208800" class="button btn-column">
        <div class="btn-firstline">
          <span class="icon">
            <img src="~/assets/images/wa.png" />
          </span>
          <span> <b>97120.8800</b> - Rayssa </span>
        </div>
        <!-- <div class="btn-secondline">
          Seg a Sex 9h às 18h e Sábado das 9h às 13h
        </div> -->
      </a>

      <a href="https://wa.me/5581993707571" class="button btn-column">
        <div class="btn-firstline">
          <span class="icon">
            <img src="~/assets/images/wa.png" />
          </span>
          <span> <b>99370.7571</b> - Mateus </span>
        </div>
        <!-- <div class="btn-secondline">
          Seg a Sex 9h às 18h e Sábado das 9h às 13h
        </div> -->
      </a>

      

      <a href="https://wa.me/5581993539678" class="button btn-column">
        <div class="btn-firstline">
          <span class="icon">
            <img src="~/assets/images/wa.png" />
          </span>
          <span> <b>99353.9678</b> - Bruno </span>
        </div>
      </a>

      <a href="https://wa.me/558196953666" class="button btn-column">
        <div class="btn-firstline">
          <span class="icon">
            <img src="~/assets/images/wa.png" />
          </span>
          <span> <b>9695.3666</b> - Carlos </span>
        </div>
        <!-- <div class="btn-secondline">
          Seg a Sex 9h às 18h e Sábado das 9h às 13h
        </div> -->
      </a>

      <!-- <a href="https://wa.me/5581997149023" class="button btn-column">
        <div class="btn-firstline">
          <span class="icon">
            <img src="~/assets/images/wa.png" />
          </span>
          <span> <b>99714.9023</b> - Brena (Assistência Técnica) </span>
        </div>
      </a> -->


      <!-- <p class="sub">Assitência Técnica</p>
      <a href="https://wa.me/558195060000" class="button btn-column">
        <div class="btn-firstline">
          <span class="icon">
            <img src="~/assets/images/wa.png">
          </span>
          <span>
            <b>9506.0000</b>
          </span>
        </div>
        <div class="btn-secondline">
          todos os dias das 9h às 19h
        </div>
      </a> -->
    </section>
  </section>
</template>

<script>
import AppLogo from "~/components/AppLogo.vue";
// import '@fortawesome/fontawesome-free-webfonts/css/fa-solid.css'

export default {
  components: {
    AppLogo
  },
  data() {
      return {
        title: '@IphonesRecifeOficial'
      }
    },
  head() {
    return {
      title: this.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: "description",
          name: "description",
          content: "iPhones Recife Oficial"
        }
      ]
    };
  }
};
</script>


