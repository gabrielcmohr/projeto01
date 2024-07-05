<template>
  <form @submit.prevent="enviar" class="form">
    <div class="info">
      <input type="text" v-model="name" minlength="3" maxlength="20" placeholder="Digite seu nome" />
      <input type="email" v-model="email" placeholder="Digite seu email" />
      <input type="date" v-model="nasc" />
    </div>

    <div class="info">
      <input required type="password" v-model="senha" placeholder="Senha" />
      <input required type="password" v-model="senha2" placeholder="Confirmar Senha" />
    </div>

    <div class="estado">
      <select v-model="EstadoFunction">
        <option disabled value="">Selecione o estado</option>
        <option v-for="(estado, index) in estados" :key="index" :value="estado.id">
          {{ estado.name }}
        </option>
      </select>
      <span>Selecionado: {{ EstadoFunction }}</span>
    </div>

    <div class="hobbies">
      <label>Qual é o seu hobby?</label>
      <div v-for="(hob, index) in hobbies" :key="index">
        <input type="radio" v-model="selecionarHob" :value="hob.id" :id="'hob-' + hob.id" />
        <label :for="'hob-' + hob.id">{{ hob.name }}</label>
      </div>
      <span>Selecionado: {{ selecionarHob }}</span>
    </div>

    <select class="ling" multiple  v-model="Linguagem">
      <label>Quais linguagens você conhece?</label>
      <option v-for="(ling, index) in linguagens" :key="index" :value="ling.id">
        <label :for="'ling-' + ling.id">{{ ling.name }}</label>
      </option>
      <span>Selecionado: {{ Linguagem }}</span>
    </select>

    <div class="bio">
      <label for="bio">Escreva sua biografia:</label>
      <textarea id="bio" v-model="texto"></textarea>
    </div>

    <div class="submit">
      <button type="submit">Enviar</button>
    </div>
  </form>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const name = ref('');
    const email = ref('');
    const nasc = ref(null);
    const texto = ref('');
    const senha = ref('');
    const senha2 = ref('');
    const EstadoFunction = ref('');
    const selecionarHob = ref(null);
    const Linguagem = ref([]);

    const linguagens = ref([
      { id: 'Python', name: 'Python' },
      { id: 'JavaScript', name: 'JavaScript' },
      { id: 'C++', name: 'C++' },
      { id: 'C', name: 'C' },
      { id: 'C#', name: 'C#' },
      { id: 'Java', name: 'Java' },
    ]);

    const estados = ref([
      { id: 'Acre', name: 'AC' },
      { id: 'Alagoas', name: 'AL' },
      { id: 'Amapá', name: 'AP' },
      { id: 'Amazonas', name: 'AM' },
      { id: 'Bahia', name: 'BA' },
      { id: 'Ceará', name: 'CE' },
      { id: 'Distrito Federal', name: 'DF' },
      { id: 'Espírito Santo', name: 'ES' },
      { id: 'Goiás', name: 'GO' },
      { id: 'Maranhão', name: 'MA' },
      { id: 'Mato Grosso', name: 'MT' },
      { id: 'Mato Grosso do Sul', name: 'MS' },
      { id: 'Minas Gerais', name: 'MG' },
      { id: 'Pará', name: 'PA' },
      { id: 'Paraíba', name: 'PB' },
      { id: 'Paraná', name: 'PR' },
      { id: 'Pernambuco', name: 'PE' },
      { id: 'Piauí', name: 'PI' },
      { id: 'Rio de Janeiro', name: 'RJ' },
      { id: 'Rio Grande do Norte', name: 'RN' },
      { id: 'Rio Grande do Sul', name: 'RS' },
      { id: 'Rondônia', name: 'RO' },
      { id: 'Roraima', name: 'RR' },
      { id: 'Santa Catarina ', name: 'SC' },
      { id: 'São Paulo', name: 'SP' },
      { id: 'Sergipe', name: 'SE' },
      { id: 'Tocantins', name: 'TO' },
    ]);

    const hobbies = ref([
      { id: 'Futebol', name: 'Futebol' },
      { id: 'Basquete', name: 'Basquete' },
      { id: 'Tênis', name: 'Tênis' },
      { id: 'Volei', name: 'Volei' },
      { id: 'Volei Areia', name: 'Volei Areia' },
    ]);

    const validarSenha = () => {
      if (senha.value === senha2.value) {
        return true;
      } else {
        alert('As senhas não coincidem');
        return false;
      }
    };

    const enviar = () => {
      if (validarSenha()) {
        const info = {
          name: name.value,
          email: email.value,
          nasc: nasc.value,
          estado: EstadoFunction.value,
          hob: selecionarHob.value,
          linguagens: Linguagem.value,
          biografia: texto.value,
        };
        alert(`Dados enviados com sucesso! \n${JSON.stringify(info, null, 2)}`);
      }
    };

    return {
      name,
      email,
      nasc,
      texto,
      senha,
      senha2,
      EstadoFunction,
      selecionarHob,
      Linguagem,
      estados,
      hobbies,
      linguagens,
      validarSenha,
      enviar,
    };
  },
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 600px;
  margin: 0 auto;
}

.info, .estado, .hobbies, .ling, .bio {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #f2f2f2;
}

.info input, .estado select, .hobbies input[type="radio"], .ling input[type="radio"], .bio textarea {
  width: 100%;
  padding: 10px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.info input[type="date"] {
  width: calc(100% - 22px); 
}

.hobbies label, .ling label {
  margin-left: 5px;
}

.submit button {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.submit button:hover {
  background-color: #45a049;
}

@media (max-width: 768px) {
  .form {
    padding: 20px;
  }
}
</style>
