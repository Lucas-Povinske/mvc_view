 <template>
  <div class="charcreate">
    <img alt="app_logo" src="../assets/logo.png">
    <div id="menu-create" style="marginTop:50px">

      <h1>Criação do Personagem</h1>
      <hr>

       <!-- CADASTRAR NOVO PERSONAGEM -->
      <form id="pers_form">
        <label for="per_nome">Nome:</label><br>
        <input type="text" id="per_nome" required autofocus v-model="cad_nome"><br>

        <label for="per_raca">Raça:</label><br>
        <!-- <vue-dropdown id="per_raca" v-model="cad_raca" :config="racalist" @setSelectedOption="setNewRaca($event);></vue-dropdown>-->

        <!--<input type="password" id="cad_senha" required autofocus v-model="cad_senha"><br>-->

        <label for="per_classe">Classe:</label><br>
        <vue-dropdown :config="classelist" @setSelectedOption="setNewClasse($event);"></vue-dropdown>

        <label for="per_hab">Habilidades:</label><br>
        <!--<label for="per_hab_forca">Força</label><br>-->


            <!--<div class="ability-score-manager-stats">-->
                <div class="ability-score-manager-stat" data-stat-id="1">
                    <div class="builder-field form-input-field">
                        <span class="builder-field-label">
                            <label for="per_forca">Força</label>
                        </span>
                        <span class="builder-field-input">
                            <input class="builder-field-value" id="qry_7" type="text" value="" required autofocus v-model="cad_for">
                        </span>
                    </div>
                </div>
                <div class="ability-score-manager-stat" data-stat-id="2"><div class="builder-field form-input-field"><span class="builder-field-label"><label for="per_destreza">Destreza</label></span><span class="builder-field-input">
                    <input class="builder-field-value" id="per_destreza" type="text" value="" required autofocus v-model="cad_des"></span></div></div>
                <div class="ability-score-manager-stat" data-stat-id="3"><div class="builder-field form-input-field"><span class="builder-field-label"><label for="per_constituicao">Constituição</label></span><span class="builder-field-input">
                    <input class="builder-field-value" id="per_constituicao" type="text" value="" required autofocus v-model="cad_con"></span></div></div>
                <div class="ability-score-manager-stat" data-stat-id="4"><div class="builder-field form-input-field"><span class="builder-field-label"><label for="per_inteligencia">Inteligência</label></span><span class="builder-field-input">
                    <input class="builder-field-value" id="per_inteligencia" type="text" value="" required autofocus v-model="cad_int"></span></div></div>
                <div class="ability-score-manager-stat" data-stat-id="5"><div class="builder-field form-input-field"><span class="builder-field-label"><label for="per_sabedoria">Sabedoria</label></span><span class="builder-field-input">
                    <input class="builder-field-value" id="per_sabedoria" type="text" value="" required autofocus v-model="cad_sab"></span></div></div>
                <div class="ability-score-manager-stat" data-stat-id="6"><div class="builder-field form-input-field"><span class="builder-field-label"><label for="per_carisma">Carisma</label></span><span class="builder-field-input">
                    <input class="builder-field-value" id="per_carisma" type="text" value="" required autofocus v-model="cad_car"></span></div></div>
            <!--</div>-->

        <label for="per_classe">Antecedente:</label><br>
        <vue-dropdown :config="antedlist" @setSelectedOption="setNewAnted($event);"></vue-dropdown>

        <label for="per_hist">Historia:</label><br>
        <input type="text" id="per_historia" required autofocus v-model="cad_historia"><br>

        <label for="per_hist">Equipamento:</label><br>
        <input type="text" id="per_historia" required autofocus v-model="cad_equipamento"><br>


        <!--<input type="text" id="cad_exibicao" required autofocus v-model="cad_exibicao">-->
        <p><button type="submit">Salvar</button></p>
      </form>

      <!-- LISTAGEM DOS USUÁRIOS 
      <table border="1" width="750px"> 
        <thead align="left">
          <tr>
            <th width="30%">Nome de Usuário</th>
            <th width="30%">Senha</th>
            <th width="40%">Nome de Exibição</th>
          </tr>
        </thead>
        <tbody align="left">
          <tr v-for=" lista in listas" :key="lista.id">
            <td>
              <img class="btn"
                src="../assets/btn_del.png"
                @click="del_show = true; del_usuario = lista.nomeUsuario">
              {{ lista.nomeUsuario }}
            </td>
            <td>
              <img class="btn"
                src="../assets/btn_put.png"
                @click="put_show = true;
                  put_type = 'senha';
                  put_usuario = lista.nomeUsuario;
                  put_exibicao = lista.nomeExibicao;
                ">
              {{ lista.senha }}
            </td>
            <td>
              <img class="btn"
                src="../assets/btn_put.png"
                @click="put_show = true;
                  put_type = 'exibicao';
                  put_usuario = lista.nomeUsuario;
                  put_senha = lista.senha;
                ">
              {{ lista.nomeExibicao }}
            </td>
          </tr>
        </tbody>
      </table>-->

      <!-- ATUALIZAÇÃO DE USUÁRIOS -->
      <div v-if="put_show" id="put_form">
        <form @submit.prevent="atualizar">
          <h4>Usuário: {{ put_usuario }}</h4>
          <div v-if="put_type == 'senha'" class="form-group" id="troca_senha">
            Nova senha:<br>
            <input type="text" id="put_senha"
            class="form-control" required autofocus
            v-model="put_senha">
          </div>
          <div v-if="put_type == 'exibicao'" class="form_group" id="troca_exibicao">
            Novo nome de exibição:<br>
            <input type="text" id="put_exibicao"
            class="form-control" required autofocus
            v-model="put_exibicao">
          </div>
          <p><button type="submit">Salvar</button></p>
        </form>
      </div>

      <!-- REMOÇÃO DE USUÁRIOS -->
      <div v-if="del_show" id="del_form">
        <form @submit.prevent="deletar">
          <h4>Digite "{{ del_usuario }}" para confirmar</h4>
          <div class="form-group"> 
              <input type="text" id="del_confirm"
              class="form-control" required autofocus
              v-model="del_confirm"> 
              <p><button type="submit">DELETAR!</button></p>
          </div>
        </form> 
      </div>

      <p id="erro">{{ cod_erro }}</p>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { mapState } from 'vuex';
import { mapGetters } from 'vuex';
import VueDropdown from 'vue-dynamic-dropdown';
export default {
  name: 'per',
  mounted(){
    this.get();
  },
  data() {
    return {
      cad_nome: '', cad_raca: '', cad_classe: '', cad_for: '', cad_des: '', cad_con: '', cad_int: '', cad_sab: '', cad_car: '', cad_historia: '', cad_equipamento: '', listas: [],
      put_show: false, put_usuario: '', put_senha: '', put_exibicao: '',
      del_show: false, del_usuario: '', del_confirm: '',
      cod_erro: '', put_type: '', showMenu: true,
      classelist: {
            options: [
                {
                    value: "Feiticeiro"
                },
                {
                    value: "Lutador"
                }
            ],
            placeholder: "Selecione uma classe",
            width: 300,
            backgroundColor: "gray"
        },
      racalist: {
            options: [
                {
                    value: "Humano"
                },
                {
                    value: "Elfo"
                },
                {
                    value: "Gnomo"
                },
            ],
            placeholder: "Selecione uma raça",
            width: 300,
            backgroundColor: "gray"
        },
        antedlist: {
            options: [
                {
                    value: "Heremita"
                },
                {
                    value: "Sábio"
                },
                {
                    value: "Órfão"
                },
            ],
            placeholder: "Selecione um antecedente",
            width: 400,
            backgroundColor: "gray"
        }
    }
  },

  components: {
    VueDropdown
  },

  computed: {
    ...mapState([
      'usuario',
      'senha'
    ]),
    ...mapGetters([
      'getUsuario',
      'getSenha'
    ])
  },

  methods: {
    cadastrar() {
      axios.post('/usuario', {
        nome: this.cad_nome,
        raca: this.RacaSelecionada,
        classe: this.ClasseSelecionada,
        anted:this.AntedSelecionado
      },
      {
        auth: { username: this.getUsuario, password: this.getSenha }
      })
      .then(res => {
        console.log(res);
        //this.listas.push(res.data);
        this.get();
      })
      .catch(error => console.log(error))
      this.cad_usuario = '';
      this.cad_senha = '';
      this.cad_exibicao = '';
    },

    atualizar(){
      axios.put('usuario?nomeUsuario=' + this.put_usuario, {
        nomeUsuario: this.put_usuario,
        senha: this.put_senha,
        nomeExibicao: this.put_exibicao
      },
      {
        auth: { username: this.getUsuario, password: this.getSenha }
      })
      .then(res => {
        console.log(res);
        this.get();
      })
      .catch(error => {
        console.log(error);
        this.erro(error.response.status);
      })
      this.put_type = '';
      this.put_senha = '';
      this.put_usuario = '';
      this.put_exibicao = '';
      this.put_show = false;
    },

    deletar(){
      if(this.del_confirm == this.del_usuario){
        axios.delete('usuario', {
          params: { "nomeUsuario" : this.del_usuario },
          headers: { Accept: 'application/json' },
          auth: { username: this.getUsuario, password: this.getSenha }
        })
        .then(res => {
          console.log(res);
          this.get();
          this.del_show = false;
        })
        .catch(error => {
          console.log(error);
          this.erro(error.response.status);
        })
        this.del_usuario = '';
        this.del_confirm = '';
      } else {
        this.cod_erro = "A confirmação não bate com o nome do usuário!";
        this.del_confirm = '';
      }
    },

    get(){
      axios.get('usuario', {
        params: { nomeUsuario: this.cad_usuario },
        headers: { Accept: 'application/json' },
        auth: { username: this.getUsuario, password: this.getSenha }
      })
      .then( res => {
        console.log(res);
        this.listas = res.data;
        this.cod_erro = '';
       })
      .catch(error => {
        console.log(error);
        this.erro(error.response.status);
      })
    },

    erro(codigo){
      switch(codigo){
        case 400: console.log('Bad request');
          break;
        case 401: console.log('Senha inválida!');
          break;
        case 404: console.log('Usuário não cadastrado!');
          break;
        default: console.log('Houston, we have a problem!');
      }
    },

    //setNewSelectedOption(selectedOption) {
      //this.racalist.placeholder = selectedOption.value;
    //},
    setNewRaca(RacaSelecionada) {
      this.racalist.placeholder = RacaSelecionada.value;
    },
    setNewClasse(ClasseSelecionada) {
      this.classelist.placeholder = ClasseSelecionada.value;
    },
    setNewAnted(AntedSelecionado) {
      this.antedlist.placeholder = AntedSelecionado.value;
    },
    }
}



</script>

<style>
  h1{ margin-bottom: 30px; }
  table{
    margin: 100%;
    background: #e4e4e4;
  }
  form{
    position: initial;
    background-color: #e4e4e486;
    height: auto;
    margin-left: auto; margin-right: auto;
  }
  img{ cursor: pointer; }
  #erro{ color: red; }
</style>