# maze
var is_start=true;
var is_end=false;
var is_cheat=false;
var is_win=true;
window.onload=function(){
	document.getElementById('start').onmouseover=function(){
		if(is_start){
			gameon();
		}else{
			init();
		}

	}
	
	
	document.getElementById('end').onmouseover=function(){
		if(is_start){
			if(is_cheat){
				gameover_cheat();
				is_start=false;
			}else if(is_win){
				console.log("win");
				gameover_win();
				is_start=false;
			}else{
				console.log("lose");
				is_start=false;
			}
		}
	}
	
}

function gameon(){
	cheat();
	onwall();	
}
function onwall(){
		var walls=document.getElementsByName('wall');
			for(var i=0;i<walls.length;i++){
			
				walls[i].onmouseover=function(){
					if(is_start){
						mouseonwall();
					}
				}
				walls[i].onmouseout=function(){
					mouseoutwall();
				}	
			
		}
	
	
}
function cheat(){
	var game_zone=document.getElementById('game_zone');
	game_zone.onmouseout = function () {
        var x = event.clientX;
        var y = event.clientY;
        var dx1 = this.offsetLeft;
        var dy1 = this.offsetTop;
        var dx2 = this.offsetLeft + this.offsetWidth;
        var dy2 = this.offsetTop + this.offsetHeight;
       	if(x<=dx1||y<=dy1||x>=dx2||y>=dy2){
       		if(is_start){
       			console.log("cheat");
       			is_cheat=true;
       			is_win=false;
       		}else{
       			is_cheat=false;
       		}
       	}else{
       		is_cheat=false;
       	}
    }
}
function gameover_win(){
		is_start=false;
		var tip=document.getElementById('tips');
		tip.innerHTML="You Win";
}
function gameover_cheat(){
	console.log("cheat");
	var tip=document.getElementById('tips');
	tip.innerHTML="Don't cheat,you should start from the 'S' and move to the 'E' inside the maze!";
}
function gameover_lose(){
	var tip=document.getElementById('tips');
	tip.innerHTML="You Lose";
	is_win=false;
	is_cheat=false;
	is_start=false;
}
function mouseonwall(){
	var wall=event.target;
	wall.style.backgroundColor="red";
	console.log("onwall");
	gameover_lose();
}

function mouseoutwall(){
	var wall=event.target;
	wall.style.backgroundColor="#E0E0E0";
}
function init(){
	var tip=document.getElementById('tips');
	tip.innerHTML="";
	is_start=true;
	is_cheat=false;
	is_end=false;
	is_win=true;
}
