
<template lang="html">
	<three-moudules  :ptotaljson="ptotaljson"
	    		:onshow="oshow"
	    		:layout="plate"
	    		:defaultValue="defaultValue"  v-on:choice-date="onOk"   v-on:cancel-date="onCancel" v-on:fouce-data="onChange" :okword="oword"  :cancelword="cword">		
	</three-moudules >
</template>

<script lang="js">
	var vm;
	module.exports ={
	    data:function(){
	    	return {
	    		ptotaljson:[],
	    		oshow:this.onshow,
	    		plate:this.layout,
	    		defaultValue:this.defaultvalue,
	    		oword:this.okword,
	    		cword:this.cancelword
	    	}
	    },
	    methods:{
	    	getJson:getJson,
	    	onChange:onChange,
	    	onOk:onOk,
	    	onCancel:onCancel
	    },
	    mounted:function(){	    	
	    	vm=this;
	    	getJson();
	    	console.log("area_",vm.defaultValue);
	    }, 
	    watch:{
	    	onshow:wonshow,
	    	defaultvalue:defaultvalue
	    },
	    props:{
	    	onshow:{
	    		type:Boolean
	    	},
	    	layout:{
	    		type:Number
	    	},
	    	okword:{
	    		type:String
	    	},
	    	cancelword:{
	    		type:String
	    	},
	    	defaultvalue:{
	    		type:String
	    	}
	    },
		components: {
			'three-moudules':require('modules/common/components/area_slide/three_modules.vue')
		}  
	}	 	 
	 
	function onCancel(data){
		vm.oshow=false;
		this.$emit('cancel-date',data);	
	}
	 
	 function onOk(data){
		 var layout=vm.plate;
		 var ptotaljson=vm.ptotaljson;
		 for(var i=0;i<ptotaljson.length;i++){
			 if(ptotaljson[i].level==1){
				 if(data.ffloor==ptotaljson[i].name){
					 data.ffloor=ptotaljson[i];
				 }
			 }
			 if(ptotaljson[i].level==2&&layout>=2){
				 if(data.sfloor==ptotaljson[i].name){
					 data.sfloor=ptotaljson[i];
				 }
			 }
			 if(ptotaljson[i].level==3&&layout==3){
				 if(data.tfloor==ptotaljson[i].name){
					 data.tfloor=ptotaljson[i];
				 }
			 }
		 }
		 vm.oshow=false;
		 this.$emit('choice-date',data);
	 }
	 
	 function onChange(data){
		 this.$emit('fouce-data',data);
	 }
	 
	function getJson(){
/*	 	 $.ajax({ 
		    type: "post", 
		    url:"http://api3.xsftest.com:88/api/common/getAllRegionList",
		    async:false, 
		    dataType: "json", 
		    success: function (data) {
		   		if(data.status!=0){
		   			alert(data.msg);
		   			return false;
		   		}
		   		console.log(data);
		   		vm.ptotaljson=data.data;		   		
		    }               		
	 	 })*/
	 	 
	 	vm.$post($App.ApiRoot+"/common/getAllRegionList").then(function(data){	
	        	if(data.status!=0){
		   			alert(data.msg);
		   			return false;
		   		}
		   		vm.ptotaljson=data.data;
	    })
	 	 
	 	 
	}
	
	function wonshow(){
		vm.oshow=this.onshow;
	}
	
	function defaultvalue(){
		var vm=this;
		vm.defaultValue=this.defaultvalue;
	}
</script>
