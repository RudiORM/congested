<script>
	import gsap from 'gsap';
	import Lenis from '@studio-freight/lenis';
	import { onMount } from 'svelte';
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger.js';

	import { TextPlugin } from 'gsap/dist/TextPlugin.js';


	import TextContent from './content/TextContent.svelte';
	import PanelContent from './content/PanelContent.svelte';
	import data from './data/data.js'

	import data_back from './data/data_back.js'

	import * as d3 from 'd3';
	import { goto } from '$app/navigation';
	import { invalidate } from "$app/navigation";


	let cw = 0

	let format = d3.format(",");

	let format_pct = d3.format(",.2f")

	let nthElement = (arr, n = 0) =>
  (n === -1 ? arr.slice(n) : arr.slice(n, n + 1))[0];

	
	let fsize = '1rem'

	let width;

	let cmax = 6;

	let rScale = d3.scaleSqrt().domain([0,1]).range([0,6]);


	setTimeout(() => {

		if (cw>700){
			width = 600
			cmax = 6.5
			fsize = '1.3rem'
		}

		if (cw<700 && cw>600){
		width = 500
		cmax = 6
		fsize = '1.3rem'
		}

		if (cw < 600){
		width = 380
		cmax = 5
		fsize = '1.2rem'

	}

	if (cw<500){
		fsize = '1.2rem'
	}

	rScale = d3.scaleSqrt().domain([0,1]).range([0,cmax]);

	 

	
		}, "10");


	$: {console.log('cmax');
console.log(cmax)}


	const height = 780;

	const margin = {

		top: 150,
		right: 0,
		bottom: 50,
		left: 0
	};

	let c = 0

	$: innerWidth = width - margin.left - margin.right;





	let increases = [{"Bicycle":1.529,"Bus, minibus or coach":0.971,"Motor car: Driver":40.399,"Motor car: Passenger":4.519,"Motorcycle or scooter":0.28,"On foot":7.726,"Other, incl. lorry":6.441,"Train, DART or LUAS":0.182},{"Bicycle":5.025,"Bus, minibus or coach":6.333,"Motor car: Driver":103.515,"Motor car: Passenger":9.818,"Motorcycle or scooter":0.848,"On foot":14.239,"Other, incl. lorry":18.642,"Train, DART or LUAS":1.755},{"Bicycle":8.09,"Bus, minibus or coach":13.748,"Motor car: Driver":181.527,"Motor car: Passenger":15.978,"Motorcycle or scooter":1.397,"On foot":23.502,"Other, incl. lorry":32.647,"Train, DART or LUAS":5.06},{"Bicycle":11.625,"Bus, minibus or coach":21.474,"Motor car: Driver":253.663,"Motor car: Passenger":21.098,"Motorcycle or scooter":1.931,"On foot":29.767,"Other, incl. lorry":43.945,"Train, DART or LUAS":8.794},{"Bicycle":15.57,"Bus, minibus or coach":27.56,"Motor car: Driver":345.488,"Motor car: Passenger":27.419,"Motorcycle or scooter":2.488,"On foot":43.844,"Other, incl. lorry":55.296,"Train, DART or LUAS":11.929},{"Bicycle":21.638,"Bus, minibus or coach":40.39,"Motor car: Driver":456.563,"Motor car: Passenger":33.724,"Motorcycle or scooter":3.212,"On foot":54.654,"Other, incl. lorry":71.746,"Train, DART or LUAS":19.227},{"Bicycle":27.369,"Bus, minibus or coach":49.832,"Motor car: Driver":574.712,"Motor car: Passenger":40.882,"Motorcycle or scooter":3.897,"On foot":76.837,"Other, incl. lorry":85.003,"Train, DART or LUAS":25.027},{"Bicycle":35.155,"Bus, minibus or coach":60.977,"Motor car: Driver":696.955,"Motor car: Passenger":47.499,"Motorcycle or scooter":4.682,"On foot":93.424,"Other, incl. lorry":97.545,"Train, DART or LUAS":32.28},{"Bicycle":39.971,"Bus, minibus or coach":67.819,"Motor car: Driver":788.348,"Motor car: Passenger":52.479,"Motorcycle or scooter":5.226,"On foot":111.452,"Other, incl. lorry":106.226,"Train, DART or LUAS":36.278},{"Bicycle":44.319,"Bus, minibus or coach":76.8,"Motor car: Driver":870.354,"Motor car: Passenger":56.529,"Motorcycle or scooter":5.693,"On foot":123.439,"Other, incl. lorry":114.871,"Train, DART or LUAS":42.812},{"Bicycle":46.294,"Bus, minibus or coach":81.072,"Motor car: Driver":912.056,"Motor car: Passenger":58.81,"Motorcycle or scooter":5.939,"On foot":130.65,"Other, incl. lorry":119.645,"Train, DART or LUAS":45.597},{"Bicycle":47.942,"Bus, minibus or coach":86.21,"Motor car: Driver":951.719,"Motor car: Passenger":60.766,"Motorcycle or scooter":6.143,"On foot":135.017,"Other, incl. lorry":124.089,"Train, DART or LUAS":48.954},{"Bicycle":49.67,"Bus, minibus or coach":89.007,"Motor car: Driver":985.797,"Motor car: Passenger":65.203,"Motorcycle or scooter":6.453,"On foot":148.585,"Other, incl. lorry":126.868,"Train, DART or LUAS":50.408},{"Bicycle":52.924,"Bus, minibus or coach":93.828,"Motor car: Driver":1028.895,"Motor car: Passenger":70.047,"Motorcycle or scooter":6.978,"On foot":159.835,"Other, incl. lorry":129.777,"Train, DART or LUAS":51.851},{"Bicycle":55.567,"Bus, minibus or coach":98.806,"Motor car: Driver":1081.88,"Motor car: Passenger":75.762,"Motorcycle or scooter":7.49,"On foot":169.468,"Other, incl. lorry":135.75,"Train, DART or LUAS":53.161},{"Bicycle":58.713,"Bus, minibus or coach":104.55,"Motor car: Driver":1136.995,"Motor car: Passenger":80.671,"Motorcycle or scooter":8.03,"On foot":175.22,"Other, incl. lorry":144.412,"Train, DART or LUAS":54.755},{"Bicycle":60.05,"Bus, minibus or coach":108.812,"Motor car: Driver":1167.537,"Motor car: Passenger":82.581,"Motorcycle or scooter":8.298,"On foot":177.015,"Other, incl. lorry":150.845,"Train, DART or LUAS":56.397},{"Bicycle":60.51,"Bus, minibus or coach":113.668,"Motor car: Driver":1184.604,"Motor car: Passenger":83.624,"Motorcycle or scooter":8.409,"On foot":177.886,"Other, incl. lorry":153.339,"Train, DART or LUAS":58.329},{"Bicycle":60.51,"Bus, minibus or coach":114.879,"Motor car: Driver":1186.91,"Motor car: Passenger":83.865,"Motorcycle or scooter":8.422,"On foot":177.886,"Other, incl. lorry":153.642,"Train, DART or LUAS":58.697},{"Bicycle":60.674,"Bus, minibus or coach":117.779,"Motor car: Driver":1196.171,"Motor car: Passenger":84.43,"Motorcycle or scooter":8.466,"On foot":178.11,"Other, incl. lorry":157.233,"Train, DART or LUAS":60.202},{"Bicycle":60.674,"Bus, minibus or coach":119.094,"Motor car: Driver":1199.484,"Motor car: Passenger":84.667,"Motorcycle or scooter":8.479,"On foot":178.11,"Other, incl. lorry":159.008,"Train, DART or LUAS":60.886}]
	
	let decreases = [{"On foot":4.805,"Bicycle":0.561,"Bus, minibus or coach":0.226,"Train, DART or LUAS":0.019,"Motorcycle or scooter":0.101,"Motor car: Driver":11.156,"Motor car: Passenger":1.622,"Other, incl. lorry":0.573},{"On foot":8.856,"Bicycle":1.845,"Bus, minibus or coach":1.473,"Train, DART or LUAS":0.181,"Motorcycle or scooter":0.306,"Motor car: Driver":28.585,"Motor car: Passenger":3.524,"Other, incl. lorry":1.658},{"On foot":10.873,"Bicycle":2.514,"Bus, minibus or coach":3.044,"Train, DART or LUAS":0.506,"Motorcycle or scooter":0.43,"Motor car: Driver":41.026,"Motor car: Passenger":4.441,"Other, incl. lorry":2.543},{"On foot":11.612,"Bicycle":2.768,"Bus, minibus or coach":3.994,"Train, DART or LUAS":0.759,"Motorcycle or scooter":0.474,"Motor car: Driver":46.728,"Motor car: Passenger":4.762,"Other, incl. lorry":2.864},{"On foot":13.268,"Bicycle":2.979,"Bus, minibus or coach":4.177,"Train, DART or LUAS":0.801,"Motorcycle or scooter":0.499,"Motor car: Driver":51.249,"Motor car: Passenger":5.118,"Other, incl. lorry":3.04},{"On foot":14.755,"Bicycle":3.413,"Bus, minibus or coach":5.606,"Train, DART or LUAS":1.183,"Motorcycle or scooter":0.553,"Motor car: Driver":60.575,"Motor car: Passenger":5.739,"Other, incl. lorry":3.777},{"On foot":15.902,"Bicycle":3.659,"Bus, minibus or coach":6.431,"Train, DART or LUAS":1.409,"Motorcycle or scooter":0.585,"Motor car: Driver":67.401,"Motor car: Passenger":6.147,"Other, incl. lorry":4.258},{"On foot":16.589,"Bicycle":3.885,"Bus, minibus or coach":6.807,"Train, DART or LUAS":1.525,"Motorcycle or scooter":0.605,"Motor car: Driver":72.162,"Motor car: Passenger":6.374,"Other, incl. lorry":4.449},{"On foot":19.016,"Bicycle":4.246,"Bus, minibus or coach":7.072,"Train, DART or LUAS":1.591,"Motorcycle or scooter":0.653,"Motor car: Driver":80.989,"Motor car: Passenger":7.135,"Other, incl. lorry":4.816},{"On foot":20.986,"Bicycle":4.908,"Bus, minibus or coach":7.789,"Train, DART or LUAS":1.763,"Motorcycle or scooter":0.739,"Motor car: Driver":93.196,"Motor car: Passenger":7.999,"Other, incl. lorry":5.455},{"On foot":22.986,"Bicycle":5.369,"Bus, minibus or coach":8.46,"Train, DART or LUAS":1.926,"Motorcycle or scooter":0.808,"Motor car: Driver":104.806,"Motor car: Passenger":8.779,"Other, incl. lorry":6.06},{"On foot":24.256,"Bicycle":5.814,"Bus, minibus or coach":9.098,"Train, DART or LUAS":2.095,"Motorcycle or scooter":0.863,"Motor car: Driver":114.804,"Motor car: Passenger":9.376,"Other, incl. lorry":6.519},{"On foot":27.852,"Bicycle":6.38,"Bus, minibus or coach":9.602,"Train, DART or LUAS":2.203,"Motorcycle or scooter":0.944,"Motor car: Driver":131.644,"Motor car: Passenger":10.784,"Other, incl. lorry":7.252},{"On foot":30.71,"Bicycle":7.345,"Bus, minibus or coach":10.958,"Train, DART or LUAS":2.506,"Motorcycle or scooter":1.071,"Motor car: Driver":154.24,"Motor car: Passenger":12.335,"Other, incl. lorry":8.46},{"On foot":33.505,"Bicycle":8.07,"Bus, minibus or coach":12.254,"Train, DART or LUAS":2.832,"Motorcycle or scooter":1.183,"Motor car: Driver":177.121,"Motor car: Passenger":13.877,"Other, incl. lorry":9.696},{"On foot":35.275,"Bicycle":8.864,"Bus, minibus or coach":13.668,"Train, DART or LUAS":3.212,"Motorcycle or scooter":1.294,"Motor car: Driver":198.231,"Motor car: Passenger":15.145,"Other, incl. lorry":10.818},{"On foot":40.669,"Bicycle":10.067,"Bus, minibus or coach":14.98,"Train, DART or LUAS":3.547,"Motorcycle or scooter":1.475,"Motor car: Driver":232.982,"Motor car: Passenger":18.284,"Other, incl. lorry":13.326},{"On foot":44.985,"Bicycle":12.194,"Bus, minibus or coach":18.382,"Train, DART or LUAS":4.506,"Motorcycle or scooter":1.759,"Motor car: Driver":278.274,"Motor car: Passenger":21.699,"Other, incl. lorry":17.392},{"On foot":49.926,"Bicycle":13.947,"Bus, minibus or coach":21.816,"Train, DART or LUAS":5.751,"Motorcycle or scooter":2.04,"Motor car: Driver":325.197,"Motor car: Passenger":25.31,"Other, incl. lorry":22.818},{"On foot":53.197,"Bicycle":16.003,"Bus, minibus or coach":25.64,"Train, DART or LUAS":7.334,"Motorcycle or scooter":2.347,"Motor car: Driver":369.619,"Motor car: Passenger":28.356,"Other, incl. lorry":28.726},{"On foot":64.567,"Bicycle":19.033,"Bus, minibus or coach":28.924,"Train, DART or LUAS":8.783,"Motorcycle or scooter":2.8,"Motor car: Driver":442.473,"Motor car: Passenger":34.366,"Other, incl. lorry":39.69},{"On foot":73.662,"Bicycle":24.28,"Bus, minibus or coach":36.847,"Train, DART or LUAS":12.384,"Motorcycle or scooter":3.474,"Motor car: Driver":536.682,"Motor car: Passenger":40.735,"Other, incl. lorry":55.772},{"On foot":92.222,"Bicycle":29.337,"Bus, minibus or coach":44.721,"Train, DART or LUAS":16.565,"Motorcycle or scooter":4.167,"Motor car: Driver":640.813,"Motor car: Passenger":47.939,"Other, incl. lorry":72.858},{"On foot":105.947,"Bicycle":36.095,"Bus, minibus or coach":55.298,"Train, DART or LUAS":22.388,"Motorcycle or scooter":4.963,"Motor car: Driver":743.605,"Motor car: Passenger":54.269,"Other, incl. lorry":89.154},{"On foot":121.975,"Bicycle":41.046,"Bus, minibus or coach":63.909,"Train, DART or LUAS":27.441,"Motorcycle or scooter":5.614,"Motor car: Driver":830.296,"Motor car: Passenger":59.991,"Other, incl. lorry":102.811},{"On foot":132.834,"Bicycle":46.548,"Bus, minibus or coach":75.668,"Train, DART or LUAS":35.465,"Motorcycle or scooter":6.283,"Motor car: Driver":916.829,"Motor car: Passenger":65.147,"Other, incl. lorry":118.953},{"On foot":139.407,"Bicycle":49.323,"Bus, minibus or coach":82.228,"Train, DART or LUAS":39.967,"Motorcycle or scooter":6.656,"Motor car: Driver":965.179,"Motor car: Passenger":67.833,"Other, incl. lorry":128.609},{"On foot":143.315,"Bicycle":51.473,"Bus, minibus or coach":90.729,"Train, DART or LUAS":46.753,"Motorcycle or scooter":6.919,"Motor car: Driver":1006.343,"Motor car: Passenger":69.804,"Other, incl. lorry":136.801},{"On foot":147.458,"Bicycle":52.646,"Bus, minibus or coach":94.359,"Train, DART or LUAS":49.496,"Motorcycle or scooter":7.097,"Motor car: Driver":1031.677,"Motor car: Passenger":71.299,"Other, incl. lorry":141.331},{"On foot":150.784,"Bicycle":54.281,"Bus, minibus or coach":99.154,"Train, DART or LUAS":53.192,"Motorcycle or scooter":7.34,"Motor car: Driver":1062.72,"Motor car: Passenger":72.87,"Other, incl. lorry":146.823},{"On foot":152.932,"Bicycle":55.03,"Bus, minibus or coach":101.908,"Train, DART or LUAS":55.062,"Motorcycle or scooter":7.479,"Motor car: Driver":1081.16,"Motor car: Passenger":73.799,"Other, incl. lorry":150.103},{"On foot":154.227,"Bicycle":55.598,"Bus, minibus or coach":103.713,"Train, DART or LUAS":56.307,"Motorcycle or scooter":7.565,"Motor car: Driver":1093.031,"Motor car: Passenger":74.364,"Other, incl. lorry":151.614},{"On foot":157.466,"Bicycle":56.079,"Bus, minibus or coach":104.674,"Train, DART or LUAS":56.837,"Motorcycle or scooter":7.644,"Motor car: Driver":1105.29,"Motor car: Passenger":75.625,"Other, incl. lorry":152.703},{"On foot":160.094,"Bicycle":56.888,"Bus, minibus or coach":106.699,"Train, DART or LUAS":57.652,"Motorcycle or scooter":7.766,"Motor car: Driver":1122.415,"Motor car: Passenger":77.039,"Other, incl. lorry":154.392},{"On foot":162.513,"Bicycle":57.336,"Bus, minibus or coach":108.295,"Train, DART or LUAS":58.188,"Motorcycle or scooter":7.839,"Motor car: Driver":1135.727,"Motor car: Passenger":78.181,"Other, incl. lorry":155.493},{"On foot":164.022,"Bicycle":57.688,"Bus, minibus or coach":109.622,"Train, DART or LUAS":58.612,"Motorcycle or scooter":7.883,"Motor car: Driver":1145.834,"Motor car: Passenger":79.008,"Other, incl. lorry":156.039},{"On foot":166.131,"Bicycle":57.964,"Bus, minibus or coach":110.35,"Train, DART or LUAS":58.796,"Motorcycle or scooter":7.923,"Motor car: Driver":1154.18,"Motor car: Passenger":79.794,"Other, incl. lorry":156.412},{"On foot":167.722,"Bicycle":58.378,"Bus, minibus or coach":111.875,"Train, DART or LUAS":59.202,"Motorcycle or scooter":7.987,"Motor car: Driver":1164.298,"Motor car: Passenger":80.601,"Other, incl. lorry":157.09},{"On foot":172.493,"Bicycle":58.976,"Bus, minibus or coach":112.999,"Train, DART or LUAS":59.461,"Motorcycle or scooter":8.113,"Motor car: Driver":1175.027,"Motor car: Passenger":82.062,"Other, incl. lorry":157.678},{"On foot":176.249,"Bicycle":60.013,"Bus, minibus or coach":114.775,"Train, DART or LUAS":59.785,"Motorcycle or scooter":8.312,"Motor car: Driver":1186.782,"Motor car: Passenger":83.552,"Other, incl. lorry":158.178},{"On foot":177.594,"Bicycle":60.486,"Bus, minibus or coach":116.322,"Train, DART or LUAS":60.112,"Motorcycle or scooter":8.422,"Motor car: Driver":1193.157,"Motor car: Passenger":84.167,"Other, incl. lorry":158.496},{"On foot":177.941,"Bicycle":60.607,"Bus, minibus or coach":117.47,"Train, DART or LUAS":60.433,"Motorcycle or scooter":8.454,"Motor car: Driver":1196.526,"Motor car: Passenger":84.388,"Other, incl. lorry":158.708},{"On foot":177.941,"Bicycle":60.607,"Bus, minibus or coach":117.651,"Train, DART or LUAS":60.485,"Motorcycle or scooter":8.455,"Motor car: Driver":1196.974,"Motor car: Passenger":84.42,"Other, incl. lorry":158.771},{"On foot":178.109,"Bicycle":60.665,"Bus, minibus or coach":118.644,"Train, DART or LUAS":60.761,"Motorcycle or scooter":8.473,"Motor car: Driver":1198.819,"Motor car: Passenger":84.596,"Other, incl. lorry":158.933},{"On foot":178.109,"Bicycle":60.665,"Bus, minibus or coach":119.094,"Train, DART or LUAS":60.887,"Motorcycle or scooter":8.478,"Motor car: Driver":1199.479,"Motor car: Passenger":84.67,"Other, incl. lorry":159.013}]


	let sqdata = [{"Means of Travel":"Motor car: Driver","Nrows":25,"Start":0,"start_new":0,"Short":"car driver"},{"Means of Travel":"Motor car: Passenger","Nrows":3,"Start":26,"start_new":44,"Short":"car passenger"},{"Means of Travel":"Other, incl. lorry","Nrows":5,"Start":30,"start_new":32,"Short":"other, incl. van"},{"Means of Travel":"Motorcycle or scooter","Nrows":1,"Start":36,"start_new":56,"Short":"motorbike"},{"Means of Travel":"Bus, minibus or coach","Nrows":5,"Start":38,"start_new":38,"Short":"bus"},{"Means of Travel":"Train, DART or LUAS","Nrows":3,"Start":44,"start_new":48,"Short":"train/tram"},{"Means of Travel":"On foot","Nrows":5,"Start":48,"start_new":26,"Short":"on foot"},{"Means of Travel":"Bicycle","Nrows":3,"Start":54,"start_new":52,"Short":"bicycle"}]
	
	
	let colors = {"Motor car: Driver":"#fb8500","Motor car: Passenger":"#fb8500","Other, incl. lorry":"#fb8500","Motorcycle or scooter":"#fb8500","Bus, minibus or coach":"#ffb703","Train, DART or LUAS":"#ffb703","On foot":"#219ebc","Bicycle":"#219ebc"}
	
	
	$: xScale = d3.scaleLinear().domain([0, 10]).range([0+margin.left, innerWidth]);
	var yScale = d3.scaleLinear().domain([60,0]).range([height+margin.top+margin.bottom,margin.top]);

	let ct

let mounted = false

let tl = null

let end = null


	if (typeof window !== 'undefined') {
		gsap.registerPlugin(ScrollTrigger);
		gsap.registerPlugin(TextPlugin);


	}

	onMount(() => {
		scrollTo(0, 0)


		// SMOOTH SCROLING LIBRARY
		const lenis = new Lenis();
		function raf(time) {
			lenis.raf(time);
			requestAnimationFrame(raf);
		}
		requestAnimationFrame(raf);


		
	

	setTimeout(() => {
mounted=true
},10)


})




$: {if(mounted==true){


	tl = gsap.timeline({ defaults: { ease: "power1.in" },
		scrollTrigger: {
			trigger: '.scroll-section-1',
			start: 'top top',
			end: '+=4000%',
			pin: true,
			scrub: 0.9,
			anticipatePin: 1,
			markers: false,
			
		}

	});

	// gsap.to("#alien", { duration: 1, morphSVG: "#circy" });



let captions = ["",'','','',
"","06:15","06:30","06:45",
"07:00","07:15","07:30","07:45",
"08:00","08:15","08:30","08:45",
"09:00","09:15","09:30","09:45",
"10:00","10:15","10:30","10:45",
"11:00","11:15","","",
"","","","",
"","11:45","11:45",
"12:00","12:15","12:30","12:45",
"13:00","13:15","13:30","13:45",
"14:00","14:15","14:30","14:45",
"15:00","15:15","15:30","15:45",
"16:00","16:15","16:30","16:45",
"17:00","17:15","17:30","17:45",
"18:00","18:15","18:30","18:45",
"19:00","19:15","19:30","19:45",
"20:00","20:15","20:30","20:45",
"21:00","21:15","21:30","21:45",
"22:00","22:15","22:30","22:45",
''





]


for (let i = 0; i < captions.length-1; i++) {
  tl.fromTo(
    '#clock',
    { text: captions[i], opacity: 1 },
    { text: captions[i+1], duration: 0, opacity: 1 },
    i+1
  );
}


sqdata.forEach(function(o,i){

// {
tl.to(
	'#back_sq_'+i,
	{
		
		width: function(d){return xScale(10)-xScale(0)-4},
		duration:2,
		delay: 0
	},
	0
);

tl.to('#text'+i,{opacity: 1, duration:1},2)

tl.to(
    '#text'+i,
    { text: o['Short'], duration:1 },

	1

  );




})


tl.to('#pannel-1', { y: -window.innerHeight * 3, duration:3 },0);

tl.to('#pannel-2', { y: -window.innerHeight * 3, duration:3 },4);

tl.to('#pannel-3', { y: -window.innerHeight * 3, duration:3 },8);

tl.to('#pannel-4', { y: -window.innerHeight * 3, duration:3 },12);

tl.to('#pannel-5', { y: -window.innerHeight * 3, duration:3 },18);

tl.to('#pannel-6', { y: -window.innerHeight * 3, duration:3 },30);

tl.to('#pannel-7', { y: -window.innerHeight * 3, duration:3 },48);

tl.to('#pannel-8', { y: -window.innerHeight * 3, duration:3 },55);

tl.to('#pannel-9', { y: -window.innerHeight * 3, duration:3 },62);


for(let o=0;o<data_back.length;o++){

	if(o<data.length){


		tl.to(
	'#dot_'+o,
	{
		 r: function(){return rScale(data[9].Size)},

		duration:0,
		
	},
1);

		


tl.to(
	'#dot_'+o,
	{
		// cx: function(){return 500+13*o.cx_final},
		 cx: function(){return width+7},

		duration:function(){return data[o].Duration+0.5*Math.random()},
		
	},
	4+data[o].Time+0.1*Math.random()
);}



tl.to(
	'#backdot_'+o,
	{
		// cx: function(){return 500+13*o.cx_final},
		 cx: function(){return xScale(10)+7},

		duration:function(){return 0},
		
	},
	3
);





tl.to(
	'#backdot_'+o,
	{
		// cx: function(){return 500+13*o.cx_final},
		 cx: function(){return -4},

		duration:function(){return data_back[o].Duration+0.5*Math.random()},
		
	},
	34+data_back[o].Time+0.1*Math.random()
);


// }

}


increases.forEach(function(d,j){

sqdata.forEach(function(o,i){

let equiv_r = rScale(d[o['Means of Travel']])
let a = equiv_r*equiv_r*Math.PI
let h = yScale(o.Nrows)-yScale(0)-3

// {
tl.to(
	'#sq_'+i,
	{
		x:-a/h,
		width:a/h,
		 
		duration:1,
		delay: 0
	},
	4+1+j
);
tl.to(
    '#pct'+i,
    { text: format(parseInt(1000*d[o['Means of Travel']])), duration:.1 },

	4+1+j

  );


tl.to(
    '#pct'+i,
    { text: format_pct((100*d[o['Means of Travel']])/2034.277)+'%', duration:1 },

	28

  );


})


})




decreases.forEach(function(d,j){

sqdata.forEach(function(o,i){

let equiv_r = rScale(d[o['Means of Travel']])
let a = equiv_r*equiv_r*Math.PI
let h = yScale(o.Nrows)-yScale(0)-3

let orig_r = rScale(increases.slice(-1)[0][o['Means of Travel']])
	let origa = orig_r*orig_r*Math.PI
	let origh = yScale(o.Nrows)-yScale(0)-3


// {

	tl.to(
    '#text'+i,
    { text: format(parseInt(1000*d[o['Means of Travel']])), duration:.1 },

	34+1+j

  );



tl.to(
	'#leftsq_'+i,
	{
		width: a/h,
		 
		duration:1,
		delay: 0
	},
	34+1+j
);


})

})



console.log(increases.slice(-1)[0] )


sqdata.forEach(function(o,i){


	let equiv_r = rScale(increases.slice(-1)[0][o['Means of Travel']])
	let a = equiv_r*equiv_r*Math.PI
	let h = yScale(o.Nrows)-yScale(0)-3

	 let w = Math.sqrt(a)

	//let w = xScale(10)-xScale(0)-3


	tl.to('#pct'+i,{opacity: 1},23)

	tl.to(
	'#sq_'+i,
	{
		opacity:0,
		duration:2,
		
	},
	30
);



tl.to(
    '#pct'+i,
    { text: o['Short'], duration:1 },

	32

  );


  tl.to(
    '#text'+i,
    { text: '', duration:1 },

	32

  );



})


tl.to(".dots", {duration: 0, r:0},
25);



sqdata.forEach(function(o,i){

tl.to(
'#sq_'+i,
{
	y: (-yScale(o.Start)+yScale(o.start_new)),
	
	duration:3,
	delay: 0
},
26
);


tl.to(
'#back_sq_'+i,
{
	y: (-yScale(o.Start)+yScale(o.start_new)),
	
	duration:3,
	delay: 0
},
26
);

tl.to(
'#text'+i,
{
	y: (-yScale(o.Start)+yScale(o.start_new)),
	
	duration:3,
	delay: 0
},
26
);


tl.to(
'#pct'+i,
{
	y: (-yScale(o.Start)+yScale(o.start_new)),
	
	duration:3,
	delay: 0
},
26
);

})

	}
}






</script>

<header>
	<h1>congested</h1>
	<h2><br>  </h2>
	<h2><br>an extraterrestrial's view on commuting in ireland</h2>

	<p><br><br>			<a target=”_blank” href='https://dataanddesign.ie/' fill='#fb8500'>
		by: rudi o'reilly meehan</a></p>

</header>
<main>

	

	<div class="content">
		<TextContent index={1} />

	</div>


	<section class="scroll-section-1"   bind:clientWidth={cw}
	>

		<svg
		{width}
		{height}
		viewBox="0 0 {width + (margin.left + margin.right)} {height + (margin.top + margin.bottom)}"
	>

	
	<rect x={margin.left} y={-margin.top-12} height={height+3*margin.top+margin.bottom} width={width} pointer-events='none' fill='whitesmoke'></rect>


		<g transform="translate({margin.left} {margin.top})">
	
			{#each data as d, i}
			
				<circle cy={yScale(data[i].cy)-margin.top} cx={-4} r={0} id={'dot_'+i} class="dots" stroke-opacity={0.5} fill-opacity={0.6} stroke={colors[d['Means of Travel']]} fill={colors[d['Means of Travel']]} stroke-width={'0px'} />

			
			{/each}
			


			{#each data_back as d, i}
			
				<circle cy={yScale(data_back[i].cy)-margin.top} cx={0} r={rScale(d.Size)} id={'backdot_'+i} class="dots2" stroke-opacity={0.5} fill-opacity={0.6} stroke={colors[d['Means of Travel']]} fill={colors[d['Means of Travel']]} stroke-width={'0px'} />

				
			{/each}

			<rect id='leftbar' x={-margin.left+xScale(0)-10} y={-margin.top/2} height={height+margin.top+margin.bottom} width={14} fill='#444'></rect>

			<rect id='rightbar' x={width} y={-margin.top/2} height={height+margin.top+margin.bottom} width={14} fill='#444'></rect>

			{#each sqdata as d, i}

			<rect y={yScale(d.Start)-margin.top-6} x={xScale(0)+4} height={yScale(d.Nrows)-yScale(0)-3} width={0} id={'back_sq_'+i} opacity={.2} fill={colors[d['Means of Travel']]} />

			<rect y={yScale(d.Start)-margin.top-6} x={width} height={yScale(d.Nrows)-yScale(0)-3} width={0} id={'sq_'+i} opacity={.4} fill={colors[d['Means of Travel']]} />

			<rect y={yScale(d.start_new)-margin.top-6} x={xScale(0)+4} height={yScale(d.Nrows)-yScale(0)-3} width={0} id={'leftsq_'+i} opacity={.4} fill={colors[d['Means of Travel']]} />

			<!-- x={-6 + xScale(10)-width/2} -->

			<foreignObject 
			width={width/2}
			height={50}
			x={xScale(0)+7}


			y={-8-12.5+yScale(d.Start)-margin.top + (yScale(d.Nrows)-yScale(0))/2}
		id={'text'+i} opacity=0 style="text-align:left;text-anchor:start;font-weight:normal;font-size:{fsize};color:{'#444'}; vertical-align: middle !important;">
			

			<div class="textlabel" style="font-weight:normal;font-size:{fsize};color:{'#444'}; vertical-align: middle !important;" >
				<span style='vertical-align: middle!important; font-weight:normal;font-size:{fsize};color:{'#444'}'>{
					d['Short']}</span>
			  </div>
			
			</foreignObject> 


			<!-- Math.round(increases.slice(-1)[0][d['Means of Travel']]/2003*10 * 100) / 10 -->



			<foreignObject 
			width={width/2}
			height={50}
			x={xScale(5)-2}
			y={-8-12.5+yScale(d.Start)-margin.top + (yScale(d.Nrows)-yScale(0))/2}
			 opacity=1 id={'pct'+i} style="text-align:right;text-anchor:end;font-weight:normal;font-size:{fsize};color:{'#444'}; vertical-align: middle;">

			  <div class="pctlabel" style="font-weight:normal;font-size:{fsize};color:{'#444'}; vertical-align: middle;" >
				<span style='vertical-align: middle;font-weight:normal;font-size:{fsize};color:{'#444'}'>{



""


				}</span>
			  </div>
			
			</foreignObject> 



			{/each}


		<text x={3+(xScale(10)-xScale(0))/2} y = {-margin.top/2-3} text-anchor='middle' font-size={'3rem'} id='clock'>{""}</text>
		<text x={0} y = {-margin.top/2-10} text-anchor='middle' font-size={'1.5rem'} >{"home"}</text>
		<text x={xScale(10)+7} y = {-margin.top/2-10} text-anchor='middle' font-size={'1.5rem'} >{"work"}</text>

	
		</g>


	</svg>

	<PanelContent xScale={xScale} index={1} />
	<PanelContent xScale={xScale} index={2} />
	<PanelContent xScale={xScale} index={3} />
	<PanelContent xScale={xScale} index={4} />
	<PanelContent xScale={xScale} index={5} />
	<PanelContent xScale={xScale} index={6} />
	<PanelContent xScale={xScale} index={7} />
	<PanelContent xScale={xScale} index={8} />
	<PanelContent xScale={xScale} index={8} />
	<PanelContent xScale={xScale} index={9} />

	</section>


	<div class="content">
		<TextContent index={2} />

	</div>



</main>

<style>

	.dots{
		fill: '#444';
		color: '#444';
	}

	/* svg {
		width: 100%;
		height: auto;
		display: block;
	
	} */

	header {
		background-color: whitesmoke;
		color:#0c120c;
		display: flex;
		text-align: center;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		height: 40vh;
		padding: 20px;
	}

	.content {
		display: flex;
		align-items: center;
		margin: 20px auto;
		flex-direction: column;
		max-width: 700px;
		text-align: justify;
		gap: 20px;
	}

	section {
		position: relative;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		overflow: hidden;
		background-color: none;
		color: #0c120c;
		text-align: center;
		background-color: whitesmoke;
	}


	@media (max-width: 768px) {
		.content {
			margin: 0 auto;
			padding: 10px;
			max-width: 100%;
			text-align: left;
		}
	}


	.textlabel {
  background-color: none;
  text-align: left;
  line-height:normal;
  display: table;
  pointer-events: none;
  height:50px;
  width: 100%;
} 

.textlabel span {
	width: 100%;
  text-anchor: start;
  text-align: left;
  vertical-align: middle;
  display: table-cell;
  padding: 0px;

}



.pctlabel {
  background-color: none;
  text-align: right;
  line-height:normal;
  display: table;
  pointer-events: none;
  height:50px;
  width: 100%;
} 

.pctlabel span {
	width: 100%;
  text-anchor: end;
  text-align: right;
  vertical-align: middle;
  display: table-cell;
  padding: 0px;

}

a, a:link, a:visited {
  color: #444;
  text-decoration: underline;

}


</style>
