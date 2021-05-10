 <template>
  <div class="charcreate">
    <img alt="app_logo" src="../assets/logo.png">
    <div id="menu-create" style="marginTop:50px">

      <h1>Criação do Personagem</h1>
      <hr><br>

       <!-- CADASTRAR NOVO PERSONAGEM -->
      <form id="pers_form">
        <div id="p_nome">
        <label for="per_nome"><h2>Nome:</h2></label>
        <input type="text" id="per_nome" required autofocus v-model="cad_nome"><br>
        </div>

        <div id="p_raca" style="margin: center">
        <label for="per_raca"><h2>Raça:</h2></label>
        <vue-dropdown id='per_raca' :config="racalist" @setSelectedOption="setNewRaca($event);"></vue-dropdown>
        </div><br>
        <!--<input type="password" id="cad_senha" required autofocus v-model="cad_senha"><br>-->

        <div id="p_classe">
        <label for="per_classe"><h2>Classe:</h2></label>
        <vue-dropdown id='per_classe' :config="classelist" @setSelectedOption="setNewClasse($event);"></vue-dropdown>
        </div><br>

        <div id="p_hab">
        <label for="per_hab"><h2>Habilidades:</h2></label>
        <!--<label for="per_hab_forca">Força</label><br>-->
        </div><br>

            <!--<div class="ability-score-manager-stats">-->

<table>
  <tr>
    <th><label for="per_forca">Força</label></th>
    <th><label for="per_destreza">Destreza</label></th>
    <th><label for="per_constituicao">Constituição</label></th>
    <th><label for="per_inteligencia">Inteligência</label></th>
    <th><label for="per_sabedoria">Sabedoria</label></th>
    <th><label for="per_carisma">Carisma</label></th>
  </tr>
  <tr>
    <td><input class="builder-field-value" id="per_forca" type="text" value="" style="width: 100px;" required autofocus v-model="cad_for"></td>
    <td><input class="builder-field-value" id="per_destreza" type="text" value="" style="width: 100px;" required autofocus v-model="cad_des"></td>
    <td><input class="builder-field-value" id="per_constituicao" type="text" value="" style="width: 100px;" required autofocus v-model="cad_con"></td>
    <td><input class="builder-field-value" id="per_inteligencia" type="text" value="" style="width: 100px;" required autofocus v-model="cad_int"></td>
    <td><input class="builder-field-value" id="per_sabedoria" type="text" value="" style="width: 100px;" required autofocus v-model="cad_sab"></td>
    <td><input class="builder-field-value" id="per_carisma" type="text" value="" style="width: 100px;" required autofocus v-model="cad_car"></td>
  </tr>
</table>
                <!--
                <div id="p_for">
                <label for="per_forca">Força</label>
                    <input class="builder-field-value" id="qry_7" type="text" value="" required autofocus v-model="cad_for">
                </div>

                <div id="p_des">
                <label for="per_destreza">Destreza</label>
                    <input class="builder-field-value" id="per_destreza" type="text" value="" required autofocus v-model="cad_des">
                </div>
                
                <label for="per_constituicao">Constituição</label>
                    <input class="builder-field-value" id="per_constituicao" type="text" value="" required autofocus v-model="cad_con">
                
                <label for="per_inteligencia">Inteligência</label>
                    <input class="builder-field-value" id="per_inteligencia" type="text" value="" required autofocus v-model="cad_int">
                
                <label for="per_sabedoria">Sabedoria</label>
                    <input class="builder-field-value" id="per_sabedoria" type="text" value="" required autofocus v-model="cad_sab">
                
                <label for="per_carisma">Carisma</label>
                    <input class="builder-field-value" id="per_carisma" type="text" value="" required autofocus v-model="cad_car">
            </div>

        <label for="per_classe">Antecedente:</label><br>
        <vue-dropdown :config="antedlist" @setSelectedOption="setNewAnted($event);"></vue-dropdown>

        <label for="per_hist">Historia:</label><br>
        <input type="text" id="per_historia" required autofocus v-model="cad_historia"><br>

        <label for="per_hist">Equipamento:</label><br>
        <input type="text" id="per_historia" required autofocus v-model="cad_equipamento"><br>-->


        <!--<input type="text" id="cad_exibicao" required autofocus v-model="cad_exibicao">-->
        <p><button type="submit">Salvar</button></p>
      </form>
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
      cad_usuario: '', cad_senha: '', cad_nome: '', cad_for: '', cad_des: '', cad_con: '', cad_int: '', cad_sab: '', cad_car: '', cad_historia: '', cad_equipamento: '', listas: [],
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
            backgroundColor: "white"
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
            backgroundColor: "white"
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
        forca:this.cad_for,
        destreza:this.cad_des,
        constituicao:this.cad_con,
        inteligencia:this.cad_int,
        sabedoria:this.cad_sab,
        carisma:this.cad_car,
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
    align-content: center;
    table-layout: fixed;
    width: 100%;
    background: transparent;
  }
  th{
    width: 50px;
    text-align: center;
    border:0px solid transparent;
    }
  form{
    align-content: center;
    position: initial;
    background-color: #85838386;
    height: auto;
    width: 100%;
    margin-left: auto; margin-right: auto;
  }
  #p_nome{
      margin-left: auto;
  }
  h2{
    font-family: Roboto,Helvetica,sans-serif;
    font-size: 20px;
    line-height: 1.2;
    color: rgb(26, 26, 26);
    text-align: center;
    margin-top: 5px;
    margin-bottom: 5px;
  }
  input[type=text] {
  width: 300px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 2px;
  border-radius: 4px;
  }
  img{ cursor: pointer; }
  #erro{ color: red; }
</style>