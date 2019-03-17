<template>
	 <div>
          <div v-for="(quest,index) in answers">
          	<label  class="form-check-label">
          	  <input  :type= 'type'
          	          class="form-check-input"
          	          :value='quest'
          	          :name='answer'
          	          @input='onInput'     
          	    >{{quest}}
          	</label>

          </div>
			


     </div>
</template>

<script>
	export default {
		props:['type','answers'],

		data(){
				return {
					answer:'',
					valid:false

				}
			},
		beforeDestroy(){

			this.$emit('getAnswerUser',{

				answer:this.answer

			})


		},
		methods: {
			onInput(e){
				this.answer = e.target.value;
				if(this.answer!==''){this.valid=true}
				this.$emit('onAnswer',{
						
						valid:this.valid

				})
				
				}
		}

	}

</script>