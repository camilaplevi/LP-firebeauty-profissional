<script lang="ts">
import { ref, defineComponent, computed, onMounted } from 'vue';
import { cardIcons } from 'src/assets/icons/CardsIcons'
import { imagesContainer } from 'src/assets/images/Images'


export default defineComponent({
  setup() {
    const titleText = ref('A beleza\ndo agora!')
    const subTitleText = ref('Mostre seu talento para o mundo inteiro. A FireBeauty é a rede social da beleza feita para quem vive da estética e quer ser visto.')
    const textListaVip = ref('Lista exclusiva. Sem spam, só beleza.')
    const textInitPage = ref('Rede Social da Beleza')
    const subTextInitPage = ref(`Criado para quem entende que ${'<strong>tempo</strong>'} \ntambém é ${'<strong>autocuidado</strong>'}.`)
    const textUnderCards = ref('Mais de 1486 pessoas já garantiram sua vaga na lista VIP de download antecipado!')
    const textListaVipSecond = ref('Lista de download VIP')
    const textAccess = ref('Acesso antecipado à versão beta profissional')
    const textDescount = ref('Oportunidades de destaque gratuito nos primeiros anúncios')
    const textMemberFounder = ref('Selo de embaixadora no perfil')
    const textPrivacy = ref('Política de privacidade')
    const textDireitos = ref('Todos os direitos reservados por FireBeauty')


    const cards = ref([
      {
        title: 'Agendamento em tempo real',
        subtitle: 'Receba agendamentos diretos, sem complicação.',
        icon: cardIcons.clock
      },
      {
        title: 'Portfólio com fotos e vídeos',
        subtitle: 'Exiba seus melhores trabalhos com mídia de alta qualidade.',
        icon: cardIcons.heart
      },
      {
        title: 'Perfil bilíngue automático',
        subtitle: 'Expanda seu alcance com tradução automática para português e inglês.',
        icon: cardIcons.web
      },
      {
        title: 'Visibilidade premium',
        subtitle: '• Fire Ads: anuncie para mais visibilidade •FireExclusive, FireFlash e FirePrime: espaços de destaque.',
        icon: cardIcons.star
      }
    ])

    onMounted(() => {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('animate');
          }
        });
      }, {
        threshold: 0.1
      });

      setTimeout(() => {
        const cards = document.querySelectorAll('.info-card');
        cards.forEach(card => observer.observe(card));
      }, 100);
    });

    const nome = ref('')
    const whatsapp = ref('')
    const tipoUsuario = ref('')
    const dropdownOpcoes = ['Profissional', 'Cliente']

    const enviarFormulario = () => {
      if (!nome.value || !whatsapp.value || !tipoUsuario.value) {
        alert('Por favor, preencha todos os campos')
        return
      }

      console.log({
        nome: nome.value,
        whatsapp: whatsapp.value,
        tipoUsuario: tipoUsuario.value
      })
    }

    const formattedUnderCards = computed(() => {
      return textUnderCards.value.replace(
        '1486 pessoas',
        '<span style="color: #AD9B8E">1486 pessoas</span>'
      );
    });

    return {
      titleText,
      subTitleText,
      nome,
      whatsapp,
      textListaVip,
      textInitPage,
      subTextInitPage,
      textUnderCards,
      formattedUnderCards,
      textListaVipSecond,
      textAccess,
      textDescount,
      textMemberFounder,
      cards,
      textPrivacy,
      textDireitos,
      imagesContainer,
      tipoUsuario,
      dropdownOpcoes,
      enviarFormulario

    }
  }
})

</script>

<template>
  <q-page class="page-content" style="background-color: #F3F3F3;">
    <div class="hero-section" style="position: relative; width: 100%;">
      <picture>
        <source media="(max-width: 768px)" :srcset="imagesContainer.firstImageMobile">
        <img :src="imagesContainer.firstImage" alt="Background" class="hero-image">
      </picture>

      <div class="hero-content">
        <h1 class="hero-title">{{ titleText }}</h1>
        <p class="hero-subtitle">{{ subTitleText }}</p>

        <div>
          <q-form class="form-card" @submit.prevent="enviarFormulario">
            <q-input outlined dense v-model="nome" class="form-input" label="Seu nome:" required style="padding: 0;" />
            <q-input outlined dense v-model="whatsapp" label="Seu WhatsApp:" required mask="(##) #####-####"
              class="form-input" />
            <q-select outlined dense v-model="tipoUsuario" :options="dropdownOpcoes" label="Selecionar"
              class="form-input" required />
            <q-btn label="Quero entrar na lista VIP!" class="form-button" />
          </q-form>

          <p class="form-disclaimer">
            <q-icon name="mdi-lock" color="#AD9B8E" size="16px" class="q-mr-xs" />
            {{ textListaVip }}
          </p>
        </div>

      </div>
    </div>

    <!-- Main Content -->
    <div class="main-content">
      <div class="section-title">
        <p class="main-title">{{ textInitPage }}</p>
        <p class="sub-title" v-html="subTextInitPage"></p>
      </div>

      <div class="cards-container">
        <q-card class="info-card" v-for="(card, index) in cards" :key="index">
          <q-card-section class="card-content">
            <img :src="card.icon" alt="Ícone" class="card-icon">
            <div class="card-text">
              <p class="card-title">{{ card.title }}</p>
              <p class="card-description">{{ card.subtitle }}</p>
            </div>
          </q-card-section>
        </q-card>
      </div>

      <div class="under-cards-section">
        <div class="decorative-rectangle"></div>
        <p class="under-cards-text" v-html="formattedUnderCards"></p>
      </div>
    </div>

    <!-- VIP Section -->
    <div class="vip-section">
      <div class="vip-image mobile-first">
        <img :src="imagesContainer.lastImage" alt="Lista VIP">
      </div>

      <div class="vip-content">
        <p class="vip-title">{{ textListaVipSecond }}</p>
        <ul class="vip-benefits">
          <li>{{ textAccess }}</li>
          <li>{{ textDescount }}</li>
          <li>{{ textMemberFounder }}</li>
        </ul>
        <q-btn class="vip-button" label="Reservar meu lugar com exclusividade" />
      </div>
    </div>
    <q-footer class="page-footer" style="position: relative;">
      <div class="footer-content">
        <img :src="imagesContainer.logo" alt="Logo FireBeauty" class="footer-logo">
        <p class="privacy-text">{{ textPrivacy }}</p>
      </div>
      <q-separator color="#D9D9D9" class="footer-separator" />
      <div style="justify-content: center; display: flex;">
        <p class="copyright-text">{{ textDireitos }}</p>
      </div>
    </q-footer>
  </q-page>
</template>

<style lang="scss" scoped>
/* Hero Section */
.hero-section {
  .hero-image {
    width: 100%;
    height: auto;
    object-fit: cover;
    margin-top: 60px;

    @media (min-width: 769px) {
      height: 680px;
    }
  }

  .hero-content {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    color: white;
    padding: 25% 12%;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    @media (min-width: 769px) {
      left: 0;
      right: 0;
      max-width: 1200px;
      margin: 0 auto;
      padding: 140px 30px;

    }
  }

  .hero-title {
    font-family: 'IvyMode';
    font-size: calc(24px + 3.5vw);
    margin: 0;
    padding: 0;
    line-height: 1.2;
    white-space: pre-line;

    @media (min-width: 600px) {
      font-size: 5.6rem;
    }

    @media (min-width: 769px) {
      font-size: 4.375rem;
      padding: 0 0 40px 100px;
      line-height: 3.75rem;
    }
  }

  .hero-subtitle {
    font-family: 'Poppins';
    white-space: pre-line;
    font-weight: 400;
    line-height: 26px;
    font-size: 12px;
    margin-left: 0;
    margin-top: 5px;
    line-height: 22px;
    width: 150px;
    color: $primary;

    @media (min-width: 400px) {
      font-size: 1.4rem;
      width: 210px;
      margin-top: 30px;
    }

    @media (min-width: 500px) {
      font-size: 1.4rem;
      width: 210px;
      margin-top: 30px;
      margin-bottom: 30%;
    }

    @media (min-width: 600px) {
      font-size: 1.6rem;
      width: 210px;
      margin-top: 30px;
      margin-bottom: 30%;
    }

    @media (min-width: 769px) {
      font-size: 1.2rem;
      margin-left: 100px;
      margin-bottom: 40px;
      width: 438px;
    }
  }

  .form-card {
    background-color: #D9D9D9;
    border-radius: 18px;
    font-family: 'Poppins';
    padding: 20px;
    width: 100%;
    max-width: 600px;
    margin-left: 0;


    @media (min-width: 769px) {
      margin-left: 100px;
      width: 380px;
    }
  }

  .form-input {
    background-color: #F5F5F5;
    border-radius: 8px;
    border: 2px solid #AD9B8E;
    margin-bottom: 16px;

    label {
      width: 30px;
    }
  }

  .form-button {
    background-color: #FFA600;
    color: #322D29;
    height: 2.8125rem;
    width: 100%;
    border-radius: 32.5px;
    font-weight: 600;
    font-size: 1rem;
    text-transform: none;

    @media (min-width: 769px) {
      width: 100%;
    }
  }

  .form-disclaimer {
    font-size: 1rem;
    display: flex;
    align-items: center;
    margin-top: 5px;
    margin-left: 0;
    color: $primary;

    @media (min-width: 769px) {
      margin-left: 100px;
      font-size: 0.8rem;
    }
  }
}

/* Main Content */
.main-content {
  padding: 32px 16px;

  @media (min-width: 769px) {
    padding: 64px 32px;
  }
}

.section-title {
  text-align: center;
  margin-bottom: 32px;

  .main-title {
    font-family: 'IvyMode';
    font-size: 2.5rem;
    color: $dark-brown;
    margin: 0;

    @media (min-width: 769px) {
      font-size: 4.375rem;
    }
  }

  .sub-title {
    font-family: 'Poppins';
    font-size: 1rem;
    color: $ligth-brown;
    margin-bottom: 16px;
    white-space: pre-line;

    @media (min-width: 769px) {
      margin-bottom: 34px;
      white-space: nowrap;
    }
  }
}

.cards-container {
  display: flex;
  flex-direction: column;
  gap: 16px;
  align-items: center;

  @media (min-width: 769px) {
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    gap: 24px;
  }
}

.info-card {
  width: 242px;
  height: 224px;
  border: 3px solid transparent;
  border-radius: 16px;
  background: linear-gradient(white, #FFF6EF) padding-box,
    linear-gradient(0deg, #E9DFD7, #AD9B8E, #E9DFD7, #AD9B8E) border-box;
  background-size: 100% 100%, 400% 400%;
  background-position: center, 0% 50%;
  background-repeat: no-repeat;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
  transition: transform 0.4s ease;

  &:hover {
    transform: translateY(-4px);
  }

  &.animate {
    animation: borderFlow 4s ease-in-out forwards;
  }

  @media (min-width: 769px) {
    width: 212px;
    height: 204px;
  }


  @keyframes borderFlow {
    0% {
      background-position: center, 0% 50%;
      background: linear-gradient(white, #FFF6EF) padding-box,
        linear-gradient(0deg, #E9DFD7, #AD9B8E, #E9DFD7, #AD9B8E) border-box;
    }

    100% {
      background-position: center, 100% 50%;
      background: linear-gradient(white, #FFF6EF) padding-box,
        linear-gradient(45deg, #AD9B8E, #E9DFD7, #AD9B8E, #E9DFD7) border-box;
    }
  }

  .card-content {
    padding: 0;
    font-family: 'Poppins';
  }

  .card-icon {
    width: 2.5rem;
    margin: 6px;
  }

  .card-text {
    padding: 10px 30px;

    @media (min-width: 769px) {
      padding: 0 30px;
    }
  }

  .card-title {
    color: $dark-brown;
    font-size: 1.8rem;
    font-weight: 400;
    line-height: 20px;
    white-space: pre-line;
    margin: 0;
    padding-bottom: 0.3125rem;

    @media (min-width: 769px) {
      font-size: 1.2rem;
      font-weight: 400;
      line-height: 20px;
    }
  }

  .card-description {
    color: $tertiary;
    font-size: 1.3rem;
    margin-top: 3px;

    @media (min-width: 769px) {
      font-size: 0.7rem;
      line-height: 15px;
    }
  }
}

.under-cards-section {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 50px 50px 0;

  @media (min-width: 769px) {
    margin-top: 90px;
  }

  .decorative-rectangle {
    width: 1.0625rem;
    height: 100px;
    background: $ligth-brown;
    margin-right: 0.75rem;
    flex-shrink: 0;

    @media (min-width: 769px) {
      height: 40px;
    }
  }

  .under-cards-text {
    font-family: 'Poppins';
    width: auto;
    font-size: 1.55rem;
    font-weight: 600;
    color: $dark-brown;
    margin: 0;

    @media (min-width: 769px) {
      width: auto;
    }
  }
}

/* VIP Section */
.vip-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  margin-top: 2.5rem;
  padding: 0 1rem;

  @media (min-width: 769px) {
    flex-direction: row;
    justify-content: center;
    align-items: flex-start;
    gap: 54px;
    padding: 0;
  }

  .vip-image {
    order: 1;
    width: 100%;
    max-width: 400px;

    @media (min-width: 769px) {
      order: 2;
    }
  }

  .vip-content {
    order: 2;
    width: 300px;
    margin-bottom: 50px;

    @media (min-width: 769px) {
      order: 1;
      width: auto;
      margin-bottom: 100px;
    }
  }

  .vip-title {
    font-family: 'IvyMode';
    font-size: 2.45rem;
    font-weight: 600;
    color: $dark-brown;
  }

  .vip-benefits {
    font-family: 'Poppins';
    font-size: 1.1rem;
    color: $tertiary;
    padding-left: 20px;

    li {
      margin-bottom: 20px;
    }
  }

  .vip-button {
    font-family: 'Poppins';
    border-radius: 25.5px;
    background: linear-gradient(90deg, #CDBDB2 0%, #E9DFD7 100%);
    width: 260px;
    text-transform: none;
    font-weight: 600;
    line-height: 1.625rem;
    font-size: 1rem;
    color: $dark-brown;
    width: 100%;

    @media (min-width: 769px) {
      width: 380px;
    }
  }

  .vip-image {
    width: 100%;
    padding: 0 20px;

    @media (min-width: 769px) {
      padding: 0;
    }

    img {
      width: 100%;

      @media (min-width: 769px) {
        width: 450px;
      }
    }
  }
}

/*Footer*/
.page-footer {
  background-color: white;
  height: auto;
  padding: 1rem 0;

  .footer-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    height: auto;
    padding: 0 1rem;

    @media (min-width: 769px) {
      flex-direction: row;
      height: 80px;
      padding: 0 100px;
    }
  }

  .footer-logo {
    width: 141px;
    height: 49px;
    margin: 0.5rem 0;

    @media (min-width: 769px) {
      margin-left: 100px;
    }
  }

  .privacy-text {
    font-family: 'Poppins';
    font-weight: 500;
    font-size: 1.5rem;
    color: $tertiary;
    margin: 0.5rem 0;

    @media (min-width: 769px) {
      padding-right: 100px;
      font-size: 1rem;
    }
  }

  .footer-separator {
    margin: 0.5rem 0;
  }

  .copyright-text {
    width: 230px;
    font-family: 'Poppins';
    color: $ligth-brown;
    text-align: center;
    padding: 0.5rem 0;

    @media (min-width: 769px) {
      width: auto;
    }
  }
}
</style>