<template class="body">
  
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Eveclass Game</h1>
      </div>
      <div class="quiz-main" v-for="(element, index) in questions.slice(a,b)" :key="index" v-show="quiz">
        <div class="box-questions">
          <h2>Questão {{b}}/{{questions.length}}</h2>
          <p style="text-align: justify; margin: 0 2%; margin-bottom: 5%">{{element.question}}</p>
        </div>
        <div class="box-suggestions">
          <ul style="margin-left: 10%">
            <li v-for="(item, index) in element.suggestions" :key="index" :class="select ? check(item) : ''" @click="selectResponse(item.suggestion)">{{item.suggestion}}</li>
          </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show">
        <h2>Parabéns você venceu !!!!!!!!</h2>
        <div class="btn-restart">
          <v-btn color="primary" nuxt to="/">Sair do Game</v-btn>
        </div>
      </div>
      <div class="quiz-footer">
        <div class="box-button">
          <button v-if="condicao" @click="voltarQuestao" :style="!next ? 'background-color: rgb(106,128,202)': ''">Voltar</button>
          <button v-if="condicao2" @click="nextQuestion" :style="next ? 'background-color: rgb(106,128,202)': ''">Avançar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InspirePage',
  data(){
    return{
      questions: [
        {
          question:'1. Você acordou na floresta tonto e com uma grande dor de cabeça, sem nenhuma'
+' memória de como foi parar ali. Um barulho cada vez mais intenso foi o que'
+' despertou você desse apagão. Após abrir os olhos e levantar-se, você observa uma'
+' manada de búfalos vindo em sua direção, a pouquíssimos metros de distância. O'
+' que você faz?'
,
          suggestions:[
            {suggestion: 'a) Corre o mais rápido possível'},
            {suggestion: 'b) Sobe na árvore',correct:true},
            {suggestion: 'c) Se finge de morto'},
          ]
        },
        {
          question:'2. Ao ver que a manada passou, você desce da árvore e começa a explorar a região'
+' em busca de respostas. Não muito distante dali, você encontra um acampamento'
+' abandonado e um bilhete com instruções, deixado para trás. Antes que você possa'
+' alcançar o bilhete, um homem aparece com uma marreta gritando e avançando em'
+' sua direção. No seu corpo a adrenalina dispara. O que você faz?',
          suggestions:[
            {suggestion: 'a) Foge para bem longe'},
            {suggestion: 'b) Pega o bilhete e foge para bem longe'},
            {suggestion: 'c) Puxa toda coragem do coração e enfrenta o homem',correct:true},
          ]
        },
        {
          question:'3. Você finalmente consegue ler o bilhete: “Vamos fazer parecer um acidente. Misture o'
+' conteúdo deste frasco na comida dele. O remédio vai começar a fazer efeito depois'
+' de 30 minutos. Quando ele estiver completamente apagado, leve-o até o pé da'
+' árvore mais alta no início da floresta e direcione a manada de búfalos em sua'
+' direção. Estaremos esperando no laboratório ao norte do acampamento.” O que'
+' você faz?'
,
          suggestions:[
            {suggestion: 'a) Foge e liga para a polícia',correct:true},
            {suggestion: 'b) Amarra o homem e vai ao laboratório'},
            {suggestion: 'c) Mata o homem, pega a marreta e vai ao laboratório'},
          ]
        },
      ],
      a:0,
      b:1,
      select: false,
      quiz: true,
      score_show: false,
      condicao: false,
      condicao2: true,
      next: false,



      itemA1: 'a) Corre o mais rápido possível',
      itemB1: 'b) Sobe na árvore',
      itemC1: 'c) Se finge de morto',
      itemA2: 'a) Foge para bem longe',
      itemB2: 'b) Pega o bilhete e foge para bem longe',
      itemC2: 'c) Puxa toda coragem do coração e enfrenta o homem',
      itemA3: 'a) Foge e liga para a polícia',
      itemB3: 'b) Amarra o homem e vai ao laboratório',
      itemC3: 'c) Mata o homem, pega a marreta e vai ao laboratório',
    }
  },
  methods:{
    selectResponse(e){
      this.select = true;
      this.next = true;

      if(e === this.itemA1){
        window.location.replace("/");
        return alert('GameOver!!!  A sua corrida não foi suficiente para superar a da manada. Você morreu atropelado.')
      } else if(e === this.itemB1){
        return alert('Parabéns!!! Você sobe na árvore e escapa por pouco da manada.')
      } else if(e === this.itemC1){
        window.location.replace("/");
        return alert('GameOver!!! Os búfalos podem até ter acreditado, mas isso não os impediu de passar por cima de você. Morreu atropelado.')
      } else if(e === this.itemA2){
        window.location.replace("/");
        return alert('GameOver!!! Você consegue fugir do local e voltar à cidade, porém sem nenhuma ideia'
+ ' de quem o atacou. Você continua tentando juntar as peças do'
+ ' quebra-cabeças. 2 semanas depois você morre atropelado, “acidentalmente”, ao sair de casa')
      } else if(e === this.itemB2){
        window.location.replace("/");
        return alert('GameOver!!! O homem lhe alcançou enquanto você tentava pegar o bilhete e lhe acertouuma marretada. Você morreu.')
      } else if(e === this.itemC2){
        return alert('Parabéns!!! Você consegue desviar da primeira marretada do homem, que fica ocioso'
+ ' por um curto período, o suficiente para você acertá-lo em cheio na cabeça e apagá-lo no chão')
      } else if(e === this.itemA3){
        this.a++;
        this.b++;
        this.select = false;
        this.condicao = false;
        this.score_show = true;
        return alert('Parabéns!!! Você informa a polícia o que aconteceu e passa a localização do'
+' laboratório. Chegando lá ela se depara com um sítio de produção de cocaína'
+' e prende todos os presentes. As evidências sugerem que você ainda pode'
+' estar em perigo, por este motivo a polícia lhe coloca no programa de'
+' proteção à testemunha e você sobrevive para vivenciar uma nova história.')
      } else if(e === this.itemB3){
        window.location.replace("/");
        return alert('GameOver!!! Você amarra o homem e se dirige ao laboratório. Você entra'
+' silenciosamente e consegue chegar ao salão principal, onde você observa'
+' aproximadamente umas 10 pessoas. Um passo em falso entrega a sua'
+' posição e você é alvejado. Você morreu.')
      } else if(e === this.itemC3){
        window.location.replace("/");
        return alert('GameOver!!! Você mata o homem, pega a marreta e se dirige ao laboratório. Ao avistar'
+' 2 guardas na entrada, confiante de si e seus feitos recentes, você corre na'
+' direção dos guardas, segurando a marreta com as duas mãos levantadas'
+' acima da sua cabeça e gritando “LEEROY JEENKINS!!!!”. Infelizmente, o'
+' efeito surpresa foi prejudicado e os guardas não tiveram dificuldade em'
+' alvejá-lo. Você morreu.')
      } 

    },

    check(status){
      if(status.correct){
        return 'correct'
      }else{
        return 'incorrect'
      }
    },

    nextQuestion(){
      if(!this.next){
        return;
      }

      if(this.questions.length - 1 === this.a){
        this.score_show = true;
        this.quiz = false;
      }else{
        this.a++;
        this.b++;
        this.select = false;
        this.condicao = true;
        this.next = false;
        if(this.b === this.questions.length){
          this.condicao2 = false;
        }
      }
    
    },

    voltarQuestao(){
        this.next = true;
        this.select = true;
        this.a--;
        this.b--;
        this.condicao2 = true; 
        if(this.a === 0){
          this.condicao = false;
        }
        if(this.questions.length - 1 === this.a){
          this.score_show = false;
        }
        
    },

    restart(){
     Object.assign(this.$data, this.$options.data()); 
    }


  }


}
</script>
<style>
  .body{
    margin: 0;
    letter-spacing: 2px;
    background-color: #363636;
  }

  .container-app{
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: center;    
  }

  .container-quiz{
    display: flex;
    width: 60%;
    height: 85%;
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto;
    flex-flow: column;
    text-align: center;
    border: 1px solid #e7eae0;
    border-radius: 10px;
    background-color: white;
    box-shadow: 1 10px 20px #cdd2d2;
  }

  .quiz-header{
    display: flex;
    width: 100%;
    height: 16%;
    border-bottom: 1px solid #e7eae0;
    justify-content: center;
    align-items: center;
    background-color: #e7eae0;
    border-radius: 10px 10px 1px 1px;
    color: #363636;
  }

  .quiz-main{
    display: flex;
    width: 100%;
    height: 70%;
    flex-flow: column;
    margin: auto;
    color: #363636;
  }

  .quiz-footer{
    display: flex;
    width: 100%;
    height: 14%;
    justify-content: center;
    border-top: 1px solid #e7eae0;
    background-color: #e7eae0;
    border-radius: 1px 1px 10px;
    color: #363636;
    margin-top: 5%;
  }

  .box-questions{
    margin-top: 20px;
    color: black;
  }

  .box-suggentions{
    display: flex;
    width: 100%;
    justify-content: center;
    margin: auto;
  }

  ul{
    display: flex;
    width: 80%;
    margin: 0;
    padding: 0;
    flex-flow: column;
  }

  ul li{
    list-style: none;
    line-height: 2;
    border: 1px solid #cdd2d2;
    margin-bottom: 20px;
    border-radius: 15px;
    cursor: pointer;
  }

  li:hover{
    background-color: #e7eae0;
  }

  .box-button{
    display: flex;
    width: 100%;
  }

  .box-button button{
    width: 150px;
    height: 35px;
    outline: none;
    border: 0;
    color: white;
    font-size: 18px;
    cursor: pointer;
    border-radius: 15px;
    margin: auto;
    background-color: #a09f9ff5;
  }

  li.correct{
    border: 1px solid #00fa9a;
    background-color: #00fa9a;
    color: white;
    font-weight: 600;
  }

  li.incorrect{
    border: 1px solid #ff7f50;
    background-color: #ff7f50;
    color: white;
    font-weight: 600;
  }

  .box-score{
    display: flex;
    width: 100%;
    height: 70%;
    flex-flow: column;
    color: #363636;
  }

  .box-score h2{
    margin-top: 10%;
  }

  .btn-restart{
    display: flex;
    width: 100%;
    height: auto;
    justify-content: center;
    margin-top:50px;
  }

  .btn-restart button{
    width: 40%;
    height: 35px;
    outline: none;
    border: 0;
    color: white;
    font-size: 18px;
    cursor: pointer;
    border-radius: 15px;
    margin: auto;
    background-color: #add8e6;
  }
</style>