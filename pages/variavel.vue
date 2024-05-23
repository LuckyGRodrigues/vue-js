<template>
  <body>
    <v-app>
      <v-container>
        <TabelaComponent
          titulo="Tabelasso"
          :items="items"
          :headers="headers"
          @editou="editItem"
          @deletou="deleteItem"
          @abrir-dialog="() => ativo = true"
        />
        <v-dialog
          v-model="ativo"
          max-width="500"
        >
          <v-card
          height="550"
          width="500"
          theme="dark">
            <v-card-title>
              {{ tituloDialog }}
            </v-card-title>
            <v-card-text>
              <v-row>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="Nome" TABELASSO

                    placeholder="nome"
                    v-model="projetos.nome">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="Descricao"
                    placeholder="descricao"
                    v-model="projetos.descricao">
                  </v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="Status"
                    placeholder="status"
                    v-model="projetos.status">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="Custo"
                    placeholder="custo"
                    v-model="projetos.custo">
                  </v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="Xp Recompensa"
                    placeholder="xp_recompensa"
                    v-model="projetos.xpRecompensa">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="Data Início"
                    placeholder="dataInicio"
                    v-model=  "projetos.dataInicio">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="Data Fim"
                    placeholder="dataFim"
                    v-model="projetos.dataFim">
                  </v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-text-field
                    variant="outlined"
                    label="1 a 10"
                    placeholder="idUsuario"
                    v-model="projetos.idUsuario">
                  </v-text-field>
                </v-col>
              </v-row>
              <v-row></v-row> 
            </v-card-text>
            <v-card-actions>
              <v-btn 
                variant="outlined" 
                class="text-none"
                @click="persist()">
                  Enviar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-container>
    </v-app>
  </body>
</template>

<script>
  export default {
    data: () =>  {
      return {
        valor: 0,
        ativo: false,
        loading: true,
        textoUsuario: null,
        projetos: {
          nome: null,
          dataInicio: null,
          dataFim: null,
        },
        search: '',
        headers: [
          {
            title: 'Identificador',
            key: 'id',
          },
          {
            title: 'nomes',
            key: 'nome',
          },
          {
            title: 'status',
            key: 'status',
          },
          {
            title: 'action',
            key: 'action',
            sortable: false,
          },
        ],
        items: [],
      }
    },

    async created(){
      await this.getItems();
    },

    computed: {
      tituloDialog: function() {
        return this.projetos.id ? 'Editar': 'Criar';
      }
    },

    watch: {
      ativo(valor) {
        if (valor == false) {
          this.resetProjetos()
        }
      }
    },

    methods: {
      async persist() {
        if (this.projetos.id) {
          const response = await this.$api.patch(`/projetos/${this.projetos.id}`, this.projetos);
        } else {
          const response = await this.$api.post('/projetos', this.projetos);
        }
        this.resetProjetos()
        await this.getItems();
      },
      editItem(item) {
        this.projetos = {
          ...item
        };
        this.ativo = true;
      },
      resetProjetos() {
        this.projetos = {
          nome: null,
          status: null,
        }
        this.ativo = false;
      },
      async getItems(){
        const response = await this.$api.get('/projetos');
          this.items = response.response;
          return response;
      },
      mudaPagina() {
        this.$router.push({ path: '/pagina'});
      },
      async deleteItem (item){
        if(confirm(`Deseja deletar?`)){ 
          const response = await this.$api.delete(`/projetos/destroy/${item.id}`)
        }if(response.type == 'error'){
          alert(response.message);
        }
      },
  }
} 
</script>  