<template>
	<div>
		
			{{answersTable}}
	</div>


</template>



<script>
	export default{

	props: ['answersUser','index'],	
	 data(){
	 	return{


	 		answersTable:{}


	 	} 

	 },

	created(){
		for (let i = 0; i < this.answersUser.length; i++) {
	 			let count = i+1; 
	 			if(typeof this.answersUser[i] == 'object'){
	 				this.answersTable[count]=[];
	 				let obg = this.answersUser[i]
	 				for(let key in obg){
	 					if(obg[key]){
	 						
	 						this.answersTable[count].push(key)
	 					}		
	 				}
				}
				if(typeof this.answersUser[i] == 'string' ){
					this.answersTable[count]= this.answersUser[i]
				}
	 		}


	}


}
	

</script>