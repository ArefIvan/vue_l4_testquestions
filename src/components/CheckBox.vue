<template>
	 <div>
          <div v-for="(value,name) in answer">
          	<label  class="form-check-label">
          	  <input  :type= 'type'
          	          class="form-check-input"
          	          
          	          v-model="answer[name]"
          	          @input='onInput'     
          	    >{{name}}
          	</label>

          </div>
			


     </div>
</template>

<script>
	export default {
		props:['type','answers'],

		data(){
				return {
					
					answer:{},
					valid:false,
					count:0,
					checkedAnswer:[],

				}
			},
		
		created(){
			for (let i = 0; i < this.answers.length; i++) {
					this.answer[this.answers[i]] = false;
				}

		},
		beforeDestroy(){

			for(let key in this.answer){

				if(this.answer[key]){
					this.checkedAnswer.push(key)
				}

			}

			this.$emit('getAnswerUser',{


				answer:this.checkedAnswer

			})


		},



		methods: {
			onInput(e){
				
				this.count = e.target.checked ? this.count+1 : this.count-1
				this.valid = this.count>=2 ? true : false ;
				
				this.$emit('onAnswer',{
						
						valid:this.valid

				})
				
				}
		}

	}

</script>