
<title>Monty Hall Problem</title>
<style type="text/css">
img {
        height: 269px;
        width: 163px;
        float:left;
}
</style>
<script type="text/javascript">

var imageArray;

var phase=1
var firstchoice
var doornotshown
var chosen
var N=3
var car = Math.floor(Math.random()*N)
var probability
  var staycorrect=0
  var stayincorrect=0
  var switchcorrect=0
  var switchincorrect=0
  var switchtrials = 0
  var staytrials = 0

window.onload=setnumberofdoors
function resetValues() {
  staycorrect=0
  document.getElementById("stay_correct").value=0
   document.getElementById("stay_incorrect").value=0
    document.getElementById("switch_correct").value=0
	  document.getElementById("switch_incorrect").value=0
	    document.getElementById("stay_proportion").value=0
		document.getElementById("switch_proportion").value=0
                document.getElementById("switch_trials").value=0
                document.getElementById("stay_trials").value=0
  stayincorrect=0
  switchcorrect=0
  switchincorrect=0
  switchtrials = 0
  staytrials = 0
}
function begin() {
	var x=1
	setnumberofdoors()
	restart()
}
function createHTML(N) {
        html=""
        for (i=0;i<N;i++) {
                html+="<img src='door.jpg' onclick='doorChosen(" + i + ")'>"
        }

        document.getElementById("alldoors").innerHTML=html

}

function doorChosen(d) {
        if (phase==1){
        firstchoice=d
                imageArray[d].src="stay.jpg"
                var doornotshown=pickDoorNotToShow(N, d, car)
                for (var i=0; i<N; i++) {
                        if (i!=d && i!=doornotshown)
                           imageArray[i].src="goat.jpg"
                           imageArray[doornotshown].src="switch.jpg"
                           }

                phase = 2

        }
        else if (phase==2) {

			var stay= (d == firstchoice)
			var correct=true
                if (d==car){
                        imageArray[car].src="car1.jpg"
                        //probability[d].presented = true
                         // alert("YOU WIN " + d + " " + firstchoice + stay)
                }
                else {
                    imageArray[d].src="goat.jpg"
                        //probability[d].presented = false
                    imageArray[car].src="car1.jpg"
					correct=false
						
                         // alert("YOU LOSE " +  d + " " + firstchoice + stay)
                }
			phase=0
			var temp
			if(stay && correct){
				temp =document.getElementById("stay_correct")
				staycorrect = parseInt(temp.value)+1
				temp.value=staycorrect
			}
			
			if(stay && !correct){
				temp =document.getElementById("stay_incorrect")
				stayincorrect = parseInt(temp.value)+1
				temp.value=stayincorrect
			}
			
			if(!stay && !correct){
				temp =document.getElementById("switch_incorrect")
				switchincorrect = parseInt(temp.value)+1
				temp.value=switchincorrect
			}
			
			if(!stay && correct){
				temp =document.getElementById("switch_correct")
				switchcorrect = parseInt(temp.value)+1
				temp.value=switchcorrect
			}
			
			if(stay) document.getElementById("stay_proportion").value=Math.round((staycorrect/(staycorrect+stayincorrect))*1000)/1000
			else document.getElementById("switch_proportion").value=Math.round((switchcorrect/(switchcorrect+switchincorrect))*1000)/1000

                        if(stay) document.getElementById("stay_trials").value = (staycorrect + stayincorrect)
                        else document.getElementById("switch_trials").value = (switchcorrect + switchincorrect)
			
			document.getElementById("again").style.visibility="visible"	
			document.getElementById("clicktobegin").style.visibility="hidden"	


        }
}

function pickDoorNotToShow(N,chosen,car) {
        if (chosen==car){
                var r=chosen
                while (r==chosen)
                                 r =Math.floor(Math.random()*N)
        }
        else {
                r=car
        }
        return r

}

function setnumberofdoors(){
        N= parseInt (document.getElementById("NofDoors").value)
        car= Math.floor(Math.random()*N)
        createHTML(N)
        phase = 1

}

/*function calcprob(p){

        probability[d].response=p


}*/


function showprob(){
var data = ""
        for (var d in probability) {
                data+=probability[d].toString() + "\n"

        }
document.getElementById("prob").value=data


}

function getImages() {
        createHTML(N)
        imageArray=document.getElementsByTagName("img")

}
/*function stayXfifty(){
for (i=0;i<=5;i++)
{

}	
	
	
}
*/
</script>

<h2>Monty Hall Simulation</h2>
 <p id="clicktobegin"><strong>Click on a door to begin the simulation.</strong></p>  
<body onload="getImages()">



<div id="alldoors"><img src="./door.jpg" onclick="doorChosen(0)"><img src="./door.jpg" onclick="doorChosen(1)"><img src="./door.jpg" onclick="doorChosen(2)"></div>

<br clear="all">
 <!-- Number of Doors &nbsp; --><input name="NumberofDoors" type="hidden" id="NofDoors" dir="ltr" value="3" size="5" onclick="this.select()" autofocus=""> 
<br>
 <input type="button" name="tryagain" id="again" value="Try Again" onclick="setnumberofdoors()" > <b>Note</b> - This will not reset your current stats.
<br>
    

<br>
 &nbsp;<b>Switch Trials</b> <br>   
     &nbsp; Number of 'Switch' Trials: <input name="type=&quot;text&quot;" id="switch_trials" size="5" value="0">
    <br>
    &nbsp; Number Correct: <input name="type=&quot;text&quot;" id="switch_correct" size="5" value="0">
     <br>
    &nbsp; Number Incorrect: <input name="type=&quot;text&quot;" id="switch_incorrect" size="5" value="0">
     <br>
    &nbsp; Proportion Correct: <input name="type=&quot;text&quot;" id="switch_proportion" size="5" value="0">
 
   <b><br>
   <br>
   &nbsp;Stay Trials</b> <br>   
   &nbsp; Number of 'Stay' Trials: <input name="type=&quot;text&quot;" id="stay_trials" size="5" value="0">
   <br>
    &nbsp; Number Correct: <input name="type=&quot;text&quot;" id="stay_correct" size="5" value="0">
     <br>
  &nbsp;   Number Incorrect: <input name="type=&quot;text&quot;" id="stay_incorrect" size="5" value="0">
     <br>
  &nbsp;   Proportion Correct: <input name="type=&quot;text&quot;" id="stay_proportion" size="5" value="0">
     <br>
    

 <!--   &nbsp;<input type="button" value="Clear Data" onclick="resetValues();setnumberofdoors()"> <br>
        &nbsp; <input type="button" value="Show Explanation" onclick="document.getElementById(&#39;explanation&#39;).style.visibility=&#39;visible&#39;">  
 
    <br><br clear="all"> -->
    <br><br>
    <b>Caution</b> - The Reset Stats <b>will</b> reset your current stats with no way to recover them. 
    <br>  Note your progess before resetting.
    <br>
    <input type="button" value="Reset Stats" onclick="resetValues();setnumberofdoors()">

   <br clear="all"><br>


<br>
This page was created using a similar simulation. Please visit the <a href="http://onlinestatbook.com"> onlinestatbook</a> site cited below for other statistical simulations and explanations. <br>
<a href="http://onlinestatbook.com/2/probability/monty_hall_demo_html5/monty_hall.html"> Original Simulation</a><br>

Online Statistics Education: A Multimedia Course of Study (http://onlinestatbook.com/). Project Leader: David M. Lane, Rice University.


</body></html>