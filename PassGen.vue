<template>
  <div class="passgen">
      <div class="container">
          <div class="ttreContent">
              <div class="ttre">PassGen</div>
              <div class="ssttre">
                  Générateur de mots de passe
              </div>
          </div>
          <div class="content_gen">
              <div class="selecteur_content flex">
                  <div class="selecteur">
                      <div class="select_text">Nombre de charactères</div>
                      <div class="number">
                          <div class="select_input nombre">
                              <div class="fleche flechehaut" @click="nbCharactereplus">
                                </div>
                            <div class="nbChara">
                                {{nbCharactere}} 
                            </div>
                            <div class="fleche flechebas" @click="nbCharacteremoins">
                            </div>
                          </div>
                      </div>
                  </div>
                  <div class="selecteur">
                      <div class="select_text">Avec des chiffres ?</div>
                      <div class="select_input">
                          <div class="activBtn" :class="{selected: withNumber}" @click="numberSelect">
                              123..
                          </div>
                      </div>
                  </div>
                  <div class="selecteur">
                      <div class="select_text">Lettres minuscules ?</div>
                      <div class="select_input">
                          <div class="activBtn" :class="{selected: withLetter}" @click="letterSelect" >
                              abc...
                          </div>
                      </div>
                  </div>
                  <div class="selecteur">
                      <div class="select_text">Lettres majuscules ?</div>
                      <div class="select_input">
                          <div class="activBtn" :class="{selected: withUpper}" @click="upperSelect">
                              ABC...
                          </div>
                      </div>
                  </div>
                  <div class="selecteur">
                      <div class="select_text">Charactères spéciaux ?</div>
                      <div class="select_input">
                          <div class="activBtn" :class="{selected: withSpecial}" @click="specialSelect">
                              @#$...
                          </div>
                      </div>
                  </div>
              </div>
              <button class="generer" @click="genereMpd">Générer</button>
              <div class="motdepass">
                  <input class="passwordgen" type="text" :value="resultat"/>
                  <button class="copiepass" @click="doCopy">Copier</button>
              </div>
              <div class="message">
                  {{error}}
              </div>
              
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'PassGen',
    data: function () {
        return {
            nbCharactere : 6,
            withNumber: true,
            withLetter: false,
            withUpper :false,
            withSpecial :false,
            i : 0,
            chiffre: ["1","2","3","4","5","6","7","8","9","0"],
            lettre: ["a","b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"],
            lettreMaj: ["A","B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"],
            caractereSpeciaux: ["&", "$", "?", "#", "@"],
            tableauDeTableau: [],
            tableauChoisie: '',
            resultat : '',
            codeACopier: '',
            error: ''
        }
    },
     methods : {
         numberSelect: function () {
             this.withNumber = !this.withNumber
         },
         letterSelect: function () {
             this.withLetter = !this.withLetter
         },
         upperSelect: function () {
             this.withUpper = !this.withUpper
         },
         specialSelect: function () {
             this.withSpecial = !this.withSpecial
         },
         nbCharactereplus: function () {
             if(this.nbCharactere < 50){
                 this.nbCharactere ++
             } 
         },
         nbCharacteremoins: function () {
             if(this.nbCharactere > 1){
                 this.nbCharactere --
             } 
         },
         genereMpd: function () {
             this.resultat = ''
             this.tableauDeTableau = []
             this.error = ''
            // verifié quel selecteur est actif

            if(this.withNumber){
                this.tableauDeTableau.push(this.chiffre)
            }if(this.withLetter){
                this.tableauDeTableau.push(this.lettre)
            }if(this.withUpper){
                this.tableauDeTableau.push(this.lettreMaj)
            }if(this.withSpecial){
                this.tableauDeTableau.push(this.caractereSpeciaux)
            }
            if(this.tableauDeTableau.length != 0){
                for(this.i= 0; this.i < this.nbCharactere; this.i++){
                this.tableauChoisie = []
                this.tableauChoisie = this.tableauDeTableau[Math.floor(Math.random() * this.tableauDeTableau.length)]
                this.resultat = this.resultat + this.tableauChoisie[Math.floor(Math.random() * this.tableauChoisie.length)]
             }
            }else{
                this.error = 'choisiez au moins un type de charactère'
            }
             
         },
         doCopy() {
            this.codeACopier = document.querySelector(".passwordgen");
            this.codeACopier.select();
            document.execCommand("copy");
            },
     }

}
</script>

<style scoped>
    .passgen{
        font-family: 'Montserrat', sans-serif;
    }
 .ttreContent{
     margin-top: 50px;
     text-align: left;
     
 }
 .ttre{
     color: #fff;
     font-size: 56px;
 }
 .ssttre{
     color: #6E6E6E;
     font-size: 18px;
     font-weight: 300;
 }
 .content_gen{
     background: #06151A;
     border-radius: 28px;
     padding: 75px;
     box-shadow: 0 3px 6px rgba(0,0,0,0.56);
     margin: 35px auto;
     max-width: 830px;
 }
 .selecteur_content.flex{
     display: flex;
     justify-content: space-between;
     flex-wrap: wrap;
 }
 .selecteur{
     width: 120px;
     font-weight: 300;
 }
 .select_input, .activBtn{
     width: 120px;
     height: 120px;
     background: #040C0F;
     color: #fff;
     font-size: 25px;
     font-weight: 700;
     margin-top: 10px;
 }
 .nombre{
     display: flex;
     align-items: stretch;
     flex-wrap: wrap;
 }
 .nbChara{
     width: 100%;
 }
 .fleche{
     width: 0;
     margin: auto;
     border-left: 10px solid transparent;
     border-right: 10px solid transparent;
     cursor: pointer;
 }
 .flechehaut{
     border-bottom: 10px solid #0029CC;
 }
  .flechebas{
     border-top: 10px solid #0029CC;
 }
 .nbChara{
     display: flex;
     justify-content: center;
     align-items: center;
 }

 .input[type=number]{
     color: #fff;
 }
 .activBtn{
     display: flex;
     justify-content: center;
     align-items: center;
     cursor: pointer;
 }
 .activBtn.selected{
     background: #0029CC;
 }
  .select_input input{
      width: 100%;
      background: #040C0F;
  }
  .generer{
      margin: 45px auto;
      background: #CC0058;
      color: #fff;
      font-size: 24px;
      border-radius: 25px;
      border: none;
      padding: 7px 30px;
      cursor: pointer;
  }
  .motdepass{
      display: flex;
  }
  .passwordgen{
    width: 100%;
    border-radius: 52px 0 0 52px;
    border:none;
    background: #061114;
    font-size: 54px;
    color: #fff;
    text-align: center;
    padding: 30px;
    box-sizing: border-box;
    height: 100px;
  }
  .copiepass{
      width: 100px;
      height: 100px;
      background: #0029CC;
      color: #fff;
      border-radius: 0 52px 52px 0;
      border:none;
      font-size: 20px;
      cursor: pointer;
  }
  .message{
      padding-top: 10px
  }
  @media screen and (max-width: 700px) {
       .passwordgen{
           font-size: 25px;
       }
  }

</style>
