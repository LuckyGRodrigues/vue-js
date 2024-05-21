<template>
  <body style="background-color: black;">
    <div style="display: flex; justify-content: center;">
      <div style="width: 50%; display: inline-block;">
        <div>
          <img src="../images/SalveMeu.png" alt="twito" >
        </div>
      </div>
      <div style="width: 50%; display: inline-block;position: relative;">
        <div style="position: absolute; left: 100px; top: 20%;">
          <h1 style="font-size: 60px; font-family: inherit;">Acontecendo agora</h1>
        </div>
      </div>
    </div>
    <v-layout>
      <template>
        <v-footer class="bg-black" style="position: absolute;">
          <v-row justify="center" no-gutters>
            <a
            v-for="link in links"
            :key="link"
            class="ml-2"
            :href="link.link"
            color="grey"
            style="font-size: 12px;"
            :class="visitade"
            >
            {{ link.nome }}
            </a>
          </v-row>
        </v-footer>
      </template>
    </v-layout>
  </body>
</template>

<script>
  export default {
    data: () => ({
      links: [
        {
          nome: 'About',
          link: 'https://google.com'
        },
        {
          nome: 'Download the X app',
          link: 'https://google.com'
        },
        {
          nome: 'Help Center',
          link: 'https://google.com'
        },
        {
          nome: 'Terms of Service',
          link: 'https://google.com'
        },
        {
          nome: 'Privacy Policy',
          link: 'https://google.com'
        },
        {
          nome: 'Cookie Policy',
          link: 'https://google.com'
        },
        {
          nome: 'Accessibility',
          link: 'https://google.com'
        },
        {
          nome: 'Ads info',
          link: 'https://google.com'
        },
        {
          nome: 'Blog',
          link: 'https://google.com'
        },
        {
          nome: 'Careers',
          link: 'https://google.com'
        },
        {
          nome: 'Brand Resources',
          link: 'https://google.com'
        },
        {
          nome: 'Advertising',
          link: 'https://google.com'
        },
        {
          nome: 'Marketing',
          link: 'https://google.com'
        },
        {
          nome: 'Download the X app',
          link: 'https://google.com'
        },
        {
          nome: 'X for Business',
          link: 'https://google.com'
        },
        {
          nome: 'Developers',
          link: 'https://google.com'
        },
        {
          nome: 'Directory',
          link: 'https://google.com'
        },
        {
          nome: 'Settings',
          link: 'https://google.com'
        },
        {
          nome: '© 2024 X Corp.',
          link: 'https://google.com'
        },
      ],
    }),
  }
</script>

<style>
  a:visited {
    text-decoration: none;
    color: grey;
  }

  .container {
    display: flex;
    height: 871px;
  }
  
  .half {
    flex: 1;
    border: 1px solid black
  }

  .half img {
    max-width: 100%;
    height: auto;
    display: block;
    margin: auto;
  }

  .font {
  display: inline-block;
  transform: scale(1, 0.8);
  color: black; 
  font-family: Helvetica;
  }
</style>