<template>
  <div>
    <div v-show = "!showEnd">
      
          <h2>{{question[num].title}}</h2>
    
          <radio-box v-if="question[num].type=='radio'"
                    :type="question[num].type"
                    :answers="question[num].answers"
                    @onAnswer="getAnswer(num,$event)"
                    @getAnswerUser='getAnswerUser($event)' >
          </radio-box>
          <check-box v-if="question[num].type=='checkbox'"
                    :type="question[num].type"
                    :answers="question[num].answers"
                    @onAnswer="getAnswer(num,$event)"
                    @getAnswerUser='getAnswerUser($event)' >
          </check-box>
           
         
           
     
        
    
         <button @click='nextQuestion'
                  class="btn btn-primary"
                  :disabled = "activeBtn"
                  
         >Next Question</button>
    
      </div>
       <div v-if="showEnd" >
           <table class="table table-bordered">
           <tr v-for="(item,index) in answersUser">
              <td>{{index + 1}}</td>
             <!--  <td v-if ="typeof item == 'object'">
                <table class="table table-bordered">
                  <tr v-for="(item,index) in item">
                    <td>{{item}}</td>
                  </tr>
              </table>
             </td> -->
             <td>{{item}}</td>
           </tr>
         </table>
       </div>
  </div>

<!--        <div>

          <h2>Тест пройден</h2>
          <button @click = "showEnd=" >Посмотреть результат</button>
    
        </div> -->

<!--         <answers-user

                      v-if="showEnd"
                     :answersUser="answersUser"
                      :index="num">
        </answers-user>
      -->
       


        
  
  </div>



</template>

<script>

import RadioBox from './components/RadioBox';
import CheckBox from './components/CheckBox';
// import AnswersUser from './components/AnswersUser'

export default {
    data(){
      return {
        question:[
            {
              type: 'radio',
              title: 'Какой тег задаёт ссылку?',
              answers: [
                'a',
                'div',
                'span',
                'img'
              ]
            },
            {
              type: 'checkbox',
              title: 'Какие из  этих тегов строчные?',
              answers: [
                'a',
                'div',
                'span',
                'img'
              ]
            },
            {
              type: 'radio',
              title: 'Как расшифровывается HTML?',
              answers: [
                'HyperThread Mask Language',
                'HyperThread Markup Language',
                'HyperText Mask Language',
                'HyperText Markup Language'
              ]
            },
            {
              type: 'checkbox',
              title: 'Какие теги появились в HTML5 ?' ,
              answers: [
                'section',
                'div',
                'header',
                'title'
              ]
            },
         ],
        num:0,
        activeBtn:true,
        showEnd:false,
        answersUser:[],
        
      }
     },

   
     methods: {

        nextQuestion(){
          this.num++;
          console.log(this.num)

         
          if(this.num > (this.question.length - 1)){

             this.num = 0;
            this.showEnd = true;
          }


          this.activeBtn= !this.activeBtn


          },

        getAnswer(index,data){
          
          
          this.activeBtn = !data.valid;
         },

        getAnswerUser(data){
           this.answersUser.push(data.answer)
          console.log(this.answersUser)

        }
        
       },
     // computed: {
     //    activeBtn(){

     //      return true
     //    }
     //  },
    components:{
       RadioBox,
       CheckBox,
       // AnswersUser

      }


 }


  
</script>

<style>

</style>
