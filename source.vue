<template>
<div class="center_wrap">
  <div class="top">
  	<div class="line1">
  		<div >品牌</div>
  		<div v-for="item in brand">
  			<input type="checkbox" :id="item.id" :value="item.id" v-model="item.state">
  			<label :for="item.id">{{item.name}}</label>
  		</div>
  	</div>
  </div>
</div>	
</template>
<script >
export default{
	data(){
		return{
			brand:[
		         {name:'全部',id:0,state:false,last_state:false},
	             {name:'tata',id:1,state:false},
	             {name:'fifa',id:2,state:false},
	             {name:'baili',id:3,state:false}           
			],
			brand_checked:[],
		}
	},
	watch:{
      'brand':{
      	handler:function(){
      		//全选
      		if(this.brand[0].state == true && this.brand[0].last_state == false){
      			this.brand.forEach(v=>{
      				v.state = true
      			})
      			this.brand[0].last_state = true  
      				
      			return
      		}
      		//去掉全选
      		if(this.brand[0].state == false && this.brand[0].last_state == true){
      			this.brand.forEach(v=>{
      				v.state = false
      			})
      			this.brand[0].last_state = false
      			
      			return
      		}       
            this.brand_checked = []
            this.brand_checked = this.brand.filter( (item,index)=>{          	
            	return item.state == true
            })
           // console.log(this.brand_checked)

            //子达到全选
      		if(this.brand[0].state == false && (this.brand_checked.length == this.brand.length-1)){
                  this.brand[0].state = true 
                  this.brand[0].last_state = true
               
                  return
      		}

      		//全选去掉子
      		if(this.brand[0].state == true && (this.brand_checked.length == this.brand.length-1)){
                  this.brand[0].state = false 
                  this.brand[0].last_state = false
                 
                  this.brand_checked = []
                  return
      		}
           
      	},
      	deep:true
      }
	},
	methods:{
		
	}
}
</script>
<style lang="scss" scoped>
.center_wrap{

}	
</style>