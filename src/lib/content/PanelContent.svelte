<script>
	export let index;
	export let xScale;


	// "the commute is back" - jen hogan, the irish times, december 2023.
	// 	<br><br><br>


	// in ireland, recent census results showed that more people are doing this than ever
	// and the average time spent doing so rose to 29.1 minutes in 2022.

	// <p>
	// 		what you might find strange is that this had all changed a few 
	// 		years ago.<br><br>
	// 	a global pandemic in 2020 meant that offices were closed
	// 	and companies realised that many jobs could now be worked remotely. 

	// 	<br><br>
	// 	however, for whatever reason, things are quickly reverting back to what 
	// 	they were before.


	// 	</p>



	$: {console.log('ja')
		console.log(xScale)}
</script>



{#if index == 1}
<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
    <p>
      

		
		<br><br>

	you split the different forms of transport 
	into 3 groups:
			<span style='color:#EDBD7F'>private</span>, 
			<span style='color:#F5D784'>public</span>, or
			<span style='color:#96C6D6'>human-powered</span>.


	

    </p>
</div>
{:else if index == 2}
	<div class="text-panel"  style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
		<p>

			you start to watch people leaving their homes. <br><br> this data is taken from the 2022 census, 
			with each large dot representing 1,000 commuters.
			<br><br>
			

	   
		</p>
	</div>
{:else if index == 3}
	<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
	
		you first notice that over 200,000 people in the country 
		are leaving home before 6:30 - nearly double that of 2011.

	</div>


	{:else if index == 4}
	<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
		<p>
			in an opinion piece for the irish times in june 2023, jennifer o'connell argued that:

			<br><br>
			<i>"for many early morning commuters, i suspect it is about 
			more freedom and more choice rather than less."</i>
			<br><br>

			o'connell's point was that since one third of the workforce work from home 
			at least one day a week, longer, earlier journeys can be more palatable.

		</p>
	</div>

	{:else if index == 5}
	<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
		<p>
			the average commute time increased to 29.1 minutes in 2022. 

			<br><br>

			commutes by <span style='color:#F5D784'>train, dart or luas</span> took the longest, with an average of 52 minutes.

			<br><br>
			
			journeys to work <span style='color:#96C6D6'>on foot</span> were the shortest, with an average journey time of 17 minutes.

		</p>
	</div>

	{:else if index == 5}
	<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
		<p>
			the average commute time increased to 29.1 minutes in 2022. 

			<br><br>

			commutes by <span style='color:#F5D784'>train, dart or luas</span> took the longest, with an average of 52 minutes.

			<br><br>
			
			journeys to work <span style='color:#96C6D6'>on foot</span> were the shortest, with an average journey time of 17 minutes.

		</p>
	</div>


	{:else if index == 6}
	<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
		<p>
			more people drive to work than take every other mode of transport combined.

			<br><br>

			this has a significant impact on ireland's congestion, infrastructure and emissions.
		</p>
	</div>


	{:else if index == 7}
	<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
		<p>
			there is a more of a spread to when commuters leave the office.

			<br><br> 23% of commuters leave the office before 4pm, while 48% left between 4-6pm.

			<br><br> 15% of commuters leave after 6pm.


		</p>

		</div>


		{:else if index == 8}
		<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
			<p>
				counties meath, kildare and wicklow have the longest commute times and the most long commutes
				of 1 hour or more.
	
	
			</p>


	</div>



	{:else if index == 9}
	<div class="text-panel" style="max-width:{0.8*(xScale(10)-xScale(0))}px" id="pannel-{index}">
		<p>

			
			most 	<span style='color:#F5D784'>public transport</span> 
			 users are aged between 25 and 44 years, 
			with 56% of <span style='color:#F5D784'>bus</span>  commuters and 62% of <span style='color:#F5D784'>train</span>  commuters coming from this age bracket.


		</p>


</div>


	



{/if}





<style>
	.text-panel {
		position: absolute;
		pointer-events: none;
		z-index: 1;
		top: 100%;
		left: 50%;
		width: 100%;
		line-height: 1.4rem;
		transform: translate(-50%, 0%);
		padding: 20px;
        color: #fff;
		background-color: #444;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
		border-radius: 4px;
		text-align: center;
	}



</style>