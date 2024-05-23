<template>
  <v-row justify="center">
    <v-col
      v-for="(variant, i) in items"
      :key="i"
      cols="12"
      md="6"
    >
      <v-card
        :color="color"
        :variant="variant"
        class="mx-auto"
        theme="dark"
        height="200"
        width="400"
      >
        <v-card-item>
          <div style="border-radius: 6px; background-color: grey;">
            <div class="text-h4  mb-1">
              {{ variant.nome }}
            </div>
            <div class="text-h6">
              {{ variant.status }}
            </div>
            <div class="text-h6">
              {{ variant.descricao }}
            </div>
          </div>
        </v-card-item>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
  export default{
    data(){
      return {
        items: [],
      }
    },

    async created(){
      await this.getItems();
    },


    methods: {
      async getItems(){
        const response = await this.$api.get('/projetos');
        this.items = response.response;
        return response;
      },
    },
  }
</script>