<template>
<button class="btn btn-success" v-show="jeuencours==false" @click="StartGame()">Let's start !</button>

<div class="border-10" v-show="jeuencours==true">
    <tr class="container d-flex justify-content-center align-items-center h-100" v-for="(unTab,index) in  tab " :key="index">
        <td v-for="(uneCase, indexC) in  unTab" :key="indexC">
          <button @click="reveal(uneCase)" v-if="uneCase.hide==true">&#127761;</button>
            <button v-else>{{  uneCase.icone }}</button>
        </td>
    </tr>
    <h1 v-show='etatgame!="NotLose"' class="text-danger">{{ etatgame }}</h1>
</div>
</template>

<script>



export default {
  name: 'App',
  data() {
    return{
      del: false,
    jeuencours: false,
    newCase: { type: Object }, hide: {type: Boolean}, value: {type: Number}, coorX: {type: Number}, coorY: {type: Number},icone: {type: String},mineA: {type: Number},
    tab: [],
    nbligne: 10,
    nbcol:20,
    nbmine: 5,
    nbminep:0,
    etatgame:'NotLose'
    }
  },
  methods: {
    StartGame(){
      this.jeuencours=true
      for (let o = 0; o < this.nbligne; o++){
        let ligne=[]
        for (let i = 0; i < this.nbcol; i++){
          ligne.push({hide:true, value:0, coorX:i,coorY: o, icone:'🌕',mineA: 0})
        }
        this.tab.push(ligne)
      }

      //Placer les mines:
      let x=this.nbmine
      while (x !=this.nbminep){
        let cX=Math.floor(Math.random() * this.nbcol);
        let cY=Math.floor(Math.random() * this.nbligne);
        let untab=this.tab[cY]
        let uneCase=untab[cX]
        if (uneCase.value!=99){
          uneCase.value=99
          uneCase.icone='⚡'
          this.nbminep++
        }

      }

      },
      
      reveal(uneCase){
        uneCase.hide=false;
        if (uneCase.value==99){
          
          this.etatgame='Lose'
          uneCase.hide=false;
        }
        else {
          let CaseA=[]
          let untab=[]
          let cX=uneCase.coorX-1
          let cY=uneCase.coorY-1
          
          if (cX!=-1 & cY!=-1){
            untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          }
          cX=uneCase.coorX
          cY=uneCase.coorY-1
          if (cY!=-1){
            untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          }
          
          cX=uneCase.coorX+1
          cY=uneCase.coorY-1
          if (cY!=-1 & cX< this.nbligne){
            untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          }
          
          cX=uneCase.coorX-1
          cY=uneCase.coorY
          
          if (cX!=-1){
            untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          }

          
          cX=uneCase.coorX+1
          cY=uneCase.coorY
          if (cX< this.nbligne){
            untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          }


          
          cX=uneCase.coorX-1
          cY=uneCase.coorY+1
          
          if (cX!=-1 & cY<this.nbligne){
            untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          }

          cX=uneCase.coorX
          cY=uneCase.coorY+1
          if (cY<this.nbligne){
            untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          } 
          cX=uneCase.coorX+1
          cY=uneCase.coorY+1
          if (cX< this.nbcol & cY<this.nbligne){
          untab=this.tab[cY]
            CaseA=untab[cX]
            if (CaseA.value !=99){
              this.reveal2(CaseA)

            } else {
              uneCase.mineA++

            }
          }

          if (uneCase.mineA!=0){  
            let mes1=uneCase.mineA
            let mes2="\uFE0F\u20E3"
            let icone=mes1 + mes2
            uneCase.icone=icone
          }

         
          
          
        }
      },

      
      reveal2(uneCase){
        if (uneCase.value!=99){ 
          
          let coorX=uneCase.coorX-1
          let untab=this.tab[uneCase.coorY]
          if (coorX!=-1){
              let uneAutreCase=untab[coorX]
              console.log(uneAutreCase)
              if(this.reveal2(uneAutreCase)=="boom"){
                uneCase.mineA++
                //uneCase.icone="\uFE0F\u20E3"

              }
              else{
                uneCase.hide=false;
              }
              
          }
          if (uneCase.mineA!=0){

          
          let mes1=uneCase.mineA
          let mes2="\uFE0F\u20E3"
          let icone=mes1 + mes2
          uneCase.icone=icone
          }
        }
        
        
  }
    
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
