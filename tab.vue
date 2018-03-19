<template>
	<div id='app'>
		
		         
          <div v-if='msg.length<=4?false:true' class='left left-1' @click='left'  @mousedown.prevent>左</div>
          <div v-if='msg.length<=4?false:true' class='right right-1' @click='right' @mousedown.prevent>右</div>
         
    <ul class='ul' :style="{width:msg.length*300+'px',left:index*-300+'px'}" id='hzs'>
        <li v-for='i in msg' class='li' ><img :src=i class='img1' :style='{transform:"scale("+transitionlast+")"}' v-drag='1'></li> 
    </ul>   
    
         
         <span class='bigs' @click='bigs' @mousedown.prevent>大</span>
         <span class='smalls' @click='smalls' @mousedown.prevent>小</span>
         <span id='op'>这是索引为1的图片</span>
         
         
    <div>
           <div class='focus'>
    	 <ul class='ul1' id='ul' :style="{width:msg.length*50+'px',left:index>=4?(index-3)*-50+'px':0}">	 	
    	<li v-for='(val,num) in msg' :class='index==num?"active":""' @click='index=num'><img :src=val class='img2'> </li>
        </ul>	
           </div> 
           
           
    <span class='left left-2' @click='left' @mousedown.prevent><</span><span class='right right-2' @click='right' @mousedown.prevent>></span>
    
    
</div>


</div>
</template>

<script>
	var Vue = require('vue').default;

Vue.directive('drag',(el,val)=>{
  //console.log(el,val)
  el.onmousedown = function(e){
    var ev = e || event;
    var l = ev.clientX - el.offsetLeft;
    var t = ev.clientY - el.offsetTop;
    document.onmousemove = function(e){
      var ev = e || event;
      el.style.left = ev.clientX - l + 'px';
      el.style.top = ev.clientY - t + 'px';
    };
    document.onmouseup = function(){
      this.onmousemove = this.onmouseup = null;
    }
    return false;
  }
})
	
	
	
	
	
export default {
  data () {
    return {
      msg: ["../img/1.jpg","../img/2.jpg","../img/3.jpg","../img/4.jpg","../img/5.jpg","../img/1.jpg","../img/2.jpg","../img/3.jpg"],
      index:0,
     transitionlast:1
    
    }
  },mounted(){							
 											
                   },
                   
  methods:{
  	left(){
  	      this.index--;
      this.index == -1 && (this.index = this.msg.length-1);
      this.transitionlast = 1;
  					op.innerHTML="这是索引为"+this.index+"的图片"
  		},
  	right(){
      this.index++;
      this.index == this.msg.length && (this.index = 0);
      this.transitionlast = 1; 
	    op.innerHTML="这是索引为"+this.index+"的图片"  
  	},
  	bigs(){

  this.transitionlast+=0.2;
  		
  	},smalls(){
   
 if(this.transitionlast<=0.4){
        alert('已经到极限了');
        return;
      }
      this.transitionlast-=0.2;

  	}

  		
  	}
  

}
</script>
 
<style>
	*{
		margin:0;padding:0;list-style: none;
	}
	#app{
width:300px;
height:300px;
margin:0 auto;
position:relative;
overflow: hidden;
	}
.active{
  border-color:orange;
}
	.ul{
		height:150px;	
		position:absolute;
		float:left;
	 	 transition:1s ease;
	}
.ul li{
		width:300px;
	  height:300px;	
	  float:left;

}
.focus{
	width:100%;
	height:50px;
	overflow: hidden;
	position: absolute;
	bottom:0;
	left:10%;
	
}
	.ul1{
		height:50px;	
		float:left;
		position:absolute;
		transition:1s ease;
	}
.ul1 li{
		width:50px;
	  height:50px;	
	  float:left;
	  margin-right:5px;
	  
}
.left,.right,.bigs,.smalls{
	z-index:999;
	color:red;
	background: #ccc;
	padding:3px;
}
.left-1{
	position: absolute;
	left:0;
	top:50%;
}
.left-2{
	position: absolute;
	left:15px;
	bottom:0px;
}
.right-1{
	position: absolute;
	right:0;
top:50%;
}
.right-2{
	position: absolute;
	right:20px;
	bottom:0px;
}
.bigs{
	position: absolute;
	right:60px;
	bottom:20%;
}
.smalls{
	position: absolute;
	right:30px;
	bottom:20%;
}
.img1{
width:90%;
	}
	.img2{
		width:100%;
	}
	.img2{
		 border:3px solid #000;
	}
	.ul1 li:hover img {
  border:3px solid yellow;
	}
	input.active{
		background: #f60;
	}
	input{
		z-index:999;
		width:15px;
		height:15px;
		outline:none;
		border:none;
		background: #ccc;
		border-radius: 50%;
		margin-right:10px;
		margin-top:-30px;
	}
	.list{
		position:absolute;
		bottom:15px;
		left:28%;
	}
 #op{
 	z-index:999;
 	background: blue;
 	color:#FFFFFF;
 	position: absolute;
 	bottom:20%;
 		left:20px;
 }
	
</style>
