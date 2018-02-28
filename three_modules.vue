<style lang="css">
._vuec .com-calendar {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 100;
    width: 100%;
    height: 100%;
    display: block;
    transition: all .5s;
    /*transform: translate(0,100%);*/
}

._vuec .scroller-component {
    display: block;
    position: relative;
    height: 170px;
    overflow: hidden;
    width: 100%;
}

._vuec .scroller-content {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    z-index: -1;
}

._vuec .scroller-mask {
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    margin: 0 auto;
    width: 100%;
    z-index: 3;
    background-image: linear-gradient(to bottom, rgba(255, 255, 255, 0.95), rgba(255, 255, 255, 0.6)),
    linear-gradient(to top, rgba(255, 255, 255, 0.95), rgba(255, 255, 255, 0.6));
    background-position: top, bottom;
    background-size: 100% 68px;
    background-repeat: no-repeat;
}

._vuec .scroller-item {
	width:100%;
    text-align: center;
    font-size: 13px;
    height: 34px;
    line-height: 34px;
    color: #000;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;    
}

._vuec .scroller-indicator {
    width: 100%;
    height: 34px;
    position: absolute;
    left: 0;
    top: 68px;
    z-index: 3;
    background-image: linear-gradient(to bottom, #d0d0d0, #d0d0d0, transparent, transparent),
    linear-gradient(to top, #d0d0d0, #d0d0d0, transparent, transparent);
    background-position: top, bottom;
    background-size: 100% 1px;
    background-repeat: no-repeat;
}

._vuec .dp-container {
    position: fixed;
    width: 100%;
    left: 0;
    bottom: 0;
    z-index: 10000;
    background-color: #fff;
    transition: transform 0.3s ease;
    transform: translateY(0);
}

._vuec .dp-mask {
    position: fixed;
    width: 100%;
    height: 100%;
    left: 0px;
    top: 0px;
    opacity: 0;
    transition: opacity 0.1s ease;
    background-color: #000;
    z-index: 9999;
}

._vuec .dp-header {
    display: flex;
    width: 100%;
    box-align: center;
    align-items: center;
    background-image: linear-gradient(to bottom, #e7e7e7, #e7e7e7, transparent, transparent);
    background-position: bottom;
    background-size: 100% 1px;
    background-repeat: no-repeat;
    font-size: 13px;
    color: #333333;
    font-family: 'PingFang SC';
}

._vuec .dp-header .dp-item {
    color: #666;
    font-size: 18px;
    height: 44px;
    line-height: 44px;
    cursor: pointer;
}

._vuec .dp-content {
/*    display: flex;*/
    width: 100%;
    box-align: center;
    align-items: center;
    padding: 10px 0;
    font-size: 0px;
}

._vuec .dp-header .dp-item,
._vuec .dp-content .dp-item {
    box-sizing: border-box;
   /* flex: 1;*/
    text-align: center;
    display: inline-block;
    width:33.33%;
}



/*#app1{
        position:absolute;
        height: 320px;
        width:100%;
        bottom: 0px;
        
        }*/

._vuec .dp-left {
    float: left;
    width: 50%;
    padding: 10px 20px;/*px*/
}

._vuec .dp-right {
    float: right;
    width: 50%;
    padding: 10px 20px;/*px*/
    text-align: right;
}
._vuec .scroller-mask-layer{
	background-color: black;
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0px;
    left: 0px;
    right: 0px;
    bottom: 0px;
    filter: alpha(opacity=50);
    -moz-opacity: 0.5;
    opacity: 0.5;
    z-index: 2;
}
._vuec .day-wheel{
        position: absolute;
        overflow: visible;
        height: 34px;
        font-size:16px;
        top:68px;
        left: 0;
        right: 0;
/*        color:$unchecked-date;*/
        -webkit-transform-style: preserve-3d;
        transform-style: preserve-3d;
   }

 ._vuec .wheel-div{
        height:34px;
        line-height: 34px;
        position: absolute;
        top:0;
        width: 100%;
        text-align: center;
        -webkit-backface-visibility: hidden;
        backface-visibility: hidden;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
 }
</style>
<template lang="html">
	<div class="_vuec">
		<div class="com-calendar"    v-show="onshow" >
			    	<div class="dp-container">
			    		<div class="dp-header">
			    			<div class="dp-left"  @click ="canceldata"  v-text="cWord">取消</div>
		                	<div class="dp-right"  @click ="choiceDate"  v-text="oWord">确定</div>  			
			    		</div>	   		
				   		<div class="dp-content"> 	   		            
				            <div class="dp-item"  v-bind:style="{width:percent+'%'}">
				              	<data-scroll :datatype="'ffloor'" :datalist="ffloorjson" :defaultdata="ffloorfouce" v-on:focus-data="getfoucedata"></data-scroll>
				            </div>
				            <div class="dp-item" v-if="plate==2||plate==3"   v-bind:style="{width:percent+'%'}" >
				            	<data-scroll :datatype="'sfloor'" :datalist="sfloorjson"  :defaultdata="sfloorfouce" v-on:focus-data="getfoucedata"></data-scroll>
				            </div>
				            <div class="dp-item" v-if="plate==3"   v-bind:style="{width:percent+'%'}" >
				            	<data-scroll :datatype="'tfloor'" :datalist="tfloorjson"  :defaultdata="tfloorfouce" v-on:focus-data="getfoucedata"></data-scroll>
				            </div>		            
			            </div>
		            </div>
		</div>
	</div>
</template>
<script lang="js">
	var ffloorjson=[];
	var sfloorjson={};
	var tfloorjson={};
	var fnamecode={};
	var snamecode={};
	var vm;
	module.exports ={
	    data:function(){
	    	return {
	    		plate:this.layout!=undefined?this.layout:3,
	    		ffloorjson:[],
	    		sfloorjson:[],
	    		tfloorjson:[],
	    		percent:33,
	    		ffloorfouce:"",
	    		sfloorfouce:"",
	    		tfloorfouce:"",
	    		inilength:4,
	    		oWord:this.okword!=undefined?this.okword:"确定",
	    	    cWord:this.cancelword!=undefined?this.cancelword:"取消",
	    	    totaljson:this.ptotaljson,
	    	    dvalue:this.defaultValue
	    	}
	    },
	    methods:{
	    	setplate:setplate,
	    	getFloorfoucejson:getFloorfoucejson,
	    	getfoucedata:getfoucedata,
	    	choiceDate:choiceDate,
	    	refresh:refresh,
	    	canceldata:canceldata,
	    	getdefaultvalue:getdefaultvalue
	    },
	    mounted:function(){
	    	vm=this;
	    	setplate();
	    	if(vm.totaljson.length!=0){
	    		refresh();	    	
	    	}	    	
	    },
	    watch:{
	    	ffloorfouce:wffloorfouce,
	    	sfloorfouce:wsfloorfouce,
	    	ptotaljson:wptotaljson,
	    	defaultValue:defaultValue
	    },
	    props:{
	    	ptotaljson:{
	    		type:Array
	    	},
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
	    	defaultValue:{
	    		type:String,
	    		default:function(){
	    			return ""
	    		}
	    	}
	    },
		components: {
	        'data-scroll':require('modules/common/components/area_slide/data_scroll.vue')
	    }	
	 }
	 
	function refresh(){
		decomposeData(vm.totaljson);
    	vm.ffloorjson=ffloorjson;
    	getdefaultvalue();    	
    	getFloorfoucejson();
	}
	
	function getdefaultvalue(){
		var dvalue=vm.dvalue;
		
		if(!dvalue){
			return false;
		}
		var dvalues=dvalue.split("-");
		var dlength=dvalues.length;
		switch (dlength)
		{
		 case 1:
		 vm.ffloorfouce=dvalues[0];
		     break;
		 case 2: 
		vm.ffloorfouce=dvalues[0];
		vm.sfloorfouce=dvalues[1];
		     break;
		  default:
	    	vm.ffloorfouce=dvalues[0];
	    	vm.sfloorfouce=dvalues[1];
	    	vm.tfloorfouce=dvalues[2];
		}
	}
	
	function setplate(){
		var plate=vm.plate;
		switch (plate)
		{
		 case 1:
			 vm.percent=100;
		     break;
		 case 2: 
			 vm.percent=49;
		      break;
		  default:
			  vm.percent=33;
		}
	}

	function wffloorfouce(){
		var inilength=vm.inilength;
		vm.sfloorjson=sfloorjson[fnamecode[vm.ffloorfouce]];
		if(vm.sfloorjson.indexOf(vm.sfloorfouce) < 0){
			if(vm.sfloorjson.length<=inilength){
				vm.sfloorfouce=vm.sfloorjson[vm.sfloorjson.length-1];
			}else{
				vm.sfloorfouce=vm.sfloorjson[inilength-1];
			}
		}
			
		vm.tfloorjson=tfloorjson[snamecode[vm.sfloorfouce]];
		if(vm.tfloorjson.indexOf(vm.tfloorfouce) < 0){
			if(vm.tfloorjson.length<=inilength){
				vm.tfloorfouce=vm.tfloorjson[vm.tfloorjson.length-1];
			}else{
				vm.tfloorfouce=vm.tfloorjson[inilength-1];
			}
		}
	}

	function wsfloorfouce(){
		var inilength=vm.inilength;
		vm.tfloorjson=tfloorjson[snamecode[vm.sfloorfouce]];
		if(vm.tfloorjson.indexOf(vm.tfloorfouce) < 0){
			if(vm.tfloorjson.length<=inilength){
				vm.tfloorfouce=vm.tfloorjson[vm.tfloorjson.length-1];
			}else{
				vm.tfloorfouce=vm.tfloorjson[inilength-1];
			}	
		}
	}

	function choiceDate(){		
		var plate=vm.plate;
		var tjson={};
		switch (plate)
		{
		 case 1:
			 tjson.ffloor=vm.ffloorfouce;
		     break;
		 case 2: 
			 tjson.ffloor=vm.ffloorfouce;
			 tjson.sfloor=vm.sfloorfouce;
		      break;
		  default:
			  tjson.ffloor=vm.ffloorfouce;
		  	  tjson.sfloor=vm.sfloorfouce;
			  tjson.tfloor=vm.tfloorfouce;
		}
		this.$emit('choice-date',tjson);
	}

	function getfoucedata(data){
		var dType=data.dType;
		var focusData=data.focusData;
		this.$emit('fouce-data',data);
		switch (dType)
		{
		 case 'ffloor':
			 vm.ffloorfouce=focusData;
		     break;
		 case 'sfloor': 
			 vm.sfloorfouce=focusData;
		     break;
		  default:
			 vm.tfloorfouce=focusData;
		}
	}

	function getFloorfoucejson(){
		var inilength=vm.inilength;
		if(vm.ffloorfouce==undefined||vm.ffloorfouce==""){			
			if(vm.ffloorjson.length<=inilength){
				vm.ffloorfouce=vm.ffloorjson[vm.ffloorjson.length-1];
			}else{
				vm.ffloorfouce=vm.ffloorjson[inilength-1];
			}
		}
		vm.sfloorjson=sfloorjson[fnamecode[vm.ffloorfouce]];
		if(vm.sfloorfouce==undefined||vm.sfloorfouce==""){			
			if(vm.sfloorjson.length<=inilength){
				vm.sfloorfouce=vm.sfloorjson[vm.sfloorjson.length-1];
			}else{
				vm.sfloorfouce=vm.sfloorjson[inilength-1];
			}
		}
		vm.tfloorjson=tfloorjson[snamecode[vm.sfloorfouce]];
		if(vm.tfloorfouce==undefined||vm.tfloorfouce==""){			
			if(vm.tfloorjson.length<=inilength){
				vm.tfloorfouce=vm.tfloorjson[vm.tfloorjson.length-1];
			}else{
				vm.tfloorfouce=vm.tfloorjson[inilength-1];
			}
		}
	}

	
	function decomposeData(data){
		 console.log(data);
		 for(var i=0;i<data.length;i++){
			 var parentCode=data[i].parentCode;
			 if(parentCode){
				 if(data[i].level==2){
					 if(sfloorjson[parentCode]){
						 sfloorjson[parentCode].push(data[i].name);
						 snamecode[data[i].name]=data[i].regionCode;
					 }else{
						 sfloorjson[parentCode]=[];
						 sfloorjson[parentCode].push(data[i].name);
						 snamecode[data[i].name]=data[i].regionCode;
					 }
				 }else{
					 if(tfloorjson[parentCode]){
						 tfloorjson[parentCode].push(data[i].name);					 
					 }else{
						 tfloorjson[parentCode]=[];
						 tfloorjson[parentCode].push(data[i].name);					 
					 } 
				 }			
			 }else{
				 ffloorjson.push(data[i].name);
				 fnamecode[data[i].name]=data[i].regionCode;			 
			 }
		}
		 console.log(sfloorjson);
		 console.log(snamecode);
		 console.log(ffloorjson);
		 console.log(fnamecode);		 
	}

	
	function wptotaljson(){
		vm.totaljson=this.ptotaljson;		
		refresh();
	}
	
	
	function canceldata(){
		var data=false;
		this.$emit('cancel-date',data);	
	}
	
	function defaultValue(){
		var vm=this;
		vm.dvalue=this.defaultValue;
	}
</script>

