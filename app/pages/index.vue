<template>
  <section class="home">
    <div class="md:py-36 mx-auto flex flex-wrap flex-col md:flex-row items-center">
      <div style="padding-bottom: 16%;" class="flex flex-col w-full xl:w-2/5 justify-center lg:items-start overflow-y-hidden">
        <p>Em breve,</br>
        você conhecerá</br>
        sua nova</br>
        agência.</p>
        <div class="subtext">Siga-nos nas nossas redes, para acompanhar nossas atividades.</br>
          E, aproveite para baixar aqui nosso Brandbook e o manual de Identidade da</br>
          agência, para conhecer o incrivel mundo de buckett. rs
        </div>
        <!-- <img :src="imageText" alt="Logo" /> -->
        <nuxt-link to="/blog" class="block font-medium ">
            <img :src="botao" class="button" alt="Logo" />
          </nuxt-link>
      </div>
      <div class="flex flex-col w-full xl:w-3/5">
        <img
          alt="Hero"
          :src="imagePc"
        />
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import settings from '@/content/settings/general.json';
@Component({
  // Called to know which transition to apply
  transition() {
    return 'slide-left';
  },
})
export default class Home extends Vue {
  welcomeText = settings.welcomeText;
  imageText = settings.imageText;
  botao = settings.botao;
  imagePc = settings.imagePc;
  get posts(): Post[] {
    return this.$store.state.posts;
  }

  isSignedUp = false;

  form = {
    email: '',
  };

  encode(data): string {
    return Object.keys(data)
      .map((key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`)
      .join('&');
  }

  validEmail(email): boolean {
    // eslint-disable-next-line
    const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(email);
  }

  async handleSubmit(): Promise<void> {
    if (!this.validEmail(this.form.email)) {
      this.$refs.emailInput.focus();
      return;
    }

    try {
      await fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode({ 'form-name': 'signups', ...this.form }),
      });

      this.isSignedUp = true;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>
<style> 

p {
   font-family: Cocogoose Pro Regular;
    font-size: 3vw;
    LINE-HEIGHT: 90%;
    padding-top: 19%;
    padding-left: 15%;
    color: #00BDBD;
}
.subtext{
  font-size: 0.6vw;
    LINE-HEIGHT: 199%;
    padding-top: 10%;
    padding-left: 15%;
}
.button{
      padding-top: 6%;
    padding-left: 15%;
    width: 69%;
}
</style>