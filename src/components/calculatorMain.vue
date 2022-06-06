<template>
    <section>
          <h1>Calculator</h1>

          <div id="divinput">
            <input id="input" :value="uservalue">
          </div>
        <div id="mainblock" :style="{'background-color': theme ? '#FC4': '#CCC'}">
          
            <div id="block1">

                <div id="numbers">
                    <button @click="modulo">%</button>
                     <button @click="clearOnce"><img src="../assets/left-arrow.png" /></button>
                     <button @click="clearAll">Clear</button>
                    <button v-for="i in 10" :key="i" @click="getNumber(10-i)" >{{10-i}} </button>
                    <button @click="dot('.')">.</button>
                     <button @click="themeClicked">Theme</button>

                </div>
            
            </div>

             <div id="block1"  >
                    
                    <div id="operators" > 

                     <button @click="plus(i)">+</button>
                     <button @click="minus(i)">-</button>
                     <button @click="multiple(i)">*</button>
                     <button @click="divide(i)">/</button>
                     <button @click="equalTo(i)">=</button>

                     

                    </div>
                 
            </div>
        </div>
    </section>
        
</template>

<script>

export default {
   data(){
       return {
           

           inital:0,
           uservalue:'0',
           theme:false
           
           
       }
   },
   methods:{
       themeClicked(){
       this.theme = !this.theme;
       
       },
       getNumber(i){
      
        if(this.uservalue=='0'){

          if( this.uservalue=='0' && i=='+' || i=='-' || i=='/' || i=='*' || i=='%' || i=='.'){
               this.uservalue += i;
               //console.log("if")
          } 
          else if(this.uservalue=='0'){
         this.uservalue =''
         this.uservalue += i
               //console.log("else if")
          }
        
       }
       else{
              this.uservalue += i
            //    console.log("else")
          }   
       },
       checkoperators(x){
           
            if(this.uservalue[this.uservalue.length-1]=='+' || this.uservalue[this.uservalue.length-1]=='-' || this.uservalue[this.uservalue.length-1]=='*' || this.uservalue[this.uservalue.length-1]=='/' ||
             this.uservalue[this.uservalue.length-1]=='%' ||  this.uservalue[this.uservalue.length-1]=='.'){
             //
            }
            else{
                this.uservalue+=x
            }
       },

       plus(){
          this.checkoperators('+')
    
       },
       minus(){
           this.checkoperators('-')

           },
       divide(){
           this.checkoperators('/')
         
           },
       modulo(){
           this.checkoperators('%')
           this.uservalue = `${parseFloat(this.uservalue)/100}`

           },
       multiple(){
           this.checkoperators('*')
           },
       dot(){
               this.checkoperators('.')
            
           },
       clearAll(){
           this.uservalue=''
           this.uservalue='0'
          },
       clearOnce(){
      
     
         this.uservalue = this.uservalue.slice(0,(this.uservalue.length-1))
         //   console.log(this.count)
          if(this.uservalue==''){
          this.uservalue='0'
          }
      
       },
       equalTo(){
      
        let operatorStore=[];
        let getAns=[]   
        console.log(this.uservalue)

        let ans= (this.uservalue.split(/[\\+\-/%\\*]/))
        // let dotAns= (this.uservalue.split('+'))
        //  dotAns= (this.uservalue.split('-'))
        //  dotAns= (this.uservalue.split('*'))
        //  dotAns= (this.uservalue.split('/'))

        // console.log('dotAns',dotAns)
        
        console.log("ans",ans)
       

        for(let i=0; i<this.uservalue.length; i++){

            if(this.uservalue[i]=='+'){
                operatorStore.push('+')
            }
            else if(this.uservalue[i]=='-'){
                operatorStore.push('-')
            }
            else if(this.uservalue[i]=='*'){
                operatorStore.push('*')
            }
            else if(this.uservalue[i]=='/'){
                operatorStore.push('/')
            } 
        }
        console.log("operator store",operatorStore)

        for(let i=0; i<ans.length; i++){
         if(i%2==1){
         getAns.push(ans[i])
         getAns.push(operatorStore[i])

         }
         else{
         getAns.push(ans[i])
         getAns.push(operatorStore[i])

         }
        }
        console.log("getAns",getAns)

        this.inital += Number(getAns[0])
        console.log(this.inital)

         for(let i=0; i<getAns.length; i++){

            if(getAns[i]=='+'){
            this.inital += Number(getAns[i+1])
            }
            else if(getAns[i]=='-'){
            this.inital -= Number(getAns[i+1])
            }
            else if(getAns[i]=='*'){
            this.inital *= Number(getAns[i+1])

            }
            else if(getAns[i]=='/'){
            this.inital /= Number(getAns[i+1])

            } 
        }
        console.log(this.inital)

        this.uservalue = this.inital.toString()
        this.inital=0;

       },
   },
}
</script>

<style scoped>

#mainblock{
margin: auto;
    border: 1px solid black;
    width: 25%;
    border-top: none;
background-color:black ;
border-bottom-left-radius: 10px;
border-bottom-right-radius: 10px;

  
}
#divinput{
     margin: auto;
    border: 1px solid black;
     width: 25%;
     height: 70px;
     border-top-left-radius: 15px;
     border-top-right-radius: 15px;
     border-bottom: none;
       background-color: black;
}
#block1{
    display: inline-block;
    vertical-align: top;
     gap: 5%;
    margin: 25px 15px 0 15px;
}
#numbers{
display: grid;
grid-template-columns: repeat(3,1fr);
vertical-align: top;
gap: 6%;

}
#numbers>button{
   
padding: 10px;
box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
border-color: white;
border-radius: 12%;

}
#numbers>button>img{
   
height: 20px;
width:20px

}
#operators>button{
    margin-bottom: 38%;
    display: block;
    text-align: center;
    width: 40px;
    height: 39px;
    border-color: white;
    border-radius: 25%;

    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
#input{
    text-align: right;
    padding-right: 10px;
    height: 40px;
    width: 270px;
    margin-top:20px;

}
/* -----------------------------------------------------------------*/
@media  screen and (max-width:500px){
#mainblock{
margin: auto;
    border: 1px solid black;
    width:70%;
    border-top: none;

border-bottom-left-radius: 10px;
border-bottom-right-radius: 10px;


}
#divinput{
     margin: auto;
    border: 1px solid black;
     width: 70%;
     height: 60px;
     border-top-left-radius: 15px;
     border-top-right-radius: 15px;
     border-bottom: none;
       background-color: black;


}
#block1{
    display: inline-block;
    vertical-align: top;
     gap: 4%;
    margin: 20px 10px 0 10px;
}
#numbers{
display: grid;
grid-template-columns: repeat(3,1fr);
vertical-align: top;
gap: 7%;

}
#numbers>button{
   
padding: 5px;
box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
border-color: white;
border-radius: 15%;

}
#numbers>button>img{
   
height: 18px;
width:18px

}
#operators>button{
    margin-bottom: 38%;
    display: block;
    text-align: center;
    width: 35px;
    height: 28px;
    border-color: white;
    border-radius: 25%;

    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
#input{
    text-align: right;
    padding-right: 10px;
    height: 30px;
    width: 200px;
    margin-top:15px;

}
}
</style>
