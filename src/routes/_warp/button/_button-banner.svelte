<script>
	import { createEventDispatcher } from 'svelte';
	import { t } from 'svelte-i18n';
	import { data as charDB } from '$lib/data/characters.json';
	import { assets } from '$lib/stores/app-store';
	import { playSfx } from '$lib/helpers/sounds/audiofx';
	import positionToStyle from '$lib/helpers/css-transformer';

	export let active = false;
	export let mode = 1;
	export let bannerData = {};

	let type, featured, content;
	$: ({ type, featured, content } = bannerData);
	$: std = !type.match(/event|group/);

	const buttonOffset = (characterName) => {
		const nullValue = { buttonOffset: {} };
		const { buttonOffset } = charDB.find(({ name }) => name === characterName) || nullValue;
		return positionToStyle(buttonOffset);
	};

	const dispatch = createEventDispatcher();
	const click = () => {
		dispatch('select', { selected: type });
		if (active) return;
		playSfx('switch-banner');
	};
</script>

<button
	class:active
	class:std
	class:mode2={mode === 2}
	class:charevents={type.match('character')}
	on:click={click}
>
	{#if mode === 2}
		<div class="ornament">
			<div class="orb-content">
				<div class="circle-right">
					<!--  -->
				</div>
				<div class="circle-left" />
			</div>
		</div>
	{/if}

	{#if mode === 1}
		<svg
			class="frame"
			style="shape-rendering:geometricPrecision; text-rendering:geometricPrecision; image-rendering:optimizeQuality; fill-rule:evenodd; clip-rule:evenodd"
			viewBox="0 0 1693.84 677.54"
		>
			<path
				class="border"
				d="M0 0l300.7 0c-0.17,1.54 -0.26,3.11 -0.26,4.71 0,20.49 14.3,37.11 31.94,37.11 17.64,0 31.94,-16.62 31.94,-37.11 0,-1.6 -0.09,-3.17 -0.26,-4.71l1329.77 0 0 677.54 -1329.7 0c0.12,-1.33 0.19,-2.69 0.19,-4.06 0,-20.49 -14.3,-37.11 -31.94,-37.11 -17.64,0 -31.94,16.61 -31.94,37.11 0,1.37 0.07,2.73 0.19,4.06l-300.63 0 0 -677.54 0 0zm24.83 26.28l260.11 0c4.85,21.57 23.93,37.68 46.73,37.68 22.8,0 41.88,-16.1 46.73,-37.68l1287.29 0 0 624.99 -1287.09 0c-4.52,-22.02 -23.81,-38.57 -46.93,-38.57 -23.11,0 -42.4,16.54 -46.92,38.57l-259.92 0 0 -624.99z"
			/>
		</svg>

		<div class="svgFill">
			{#if std || type === 'lightcone-group'}
				<svg
					class="stellar"
					style="shape-rendering:geometricPrecision; text-rendering:geometricPrecision; image-rendering:optimizeQuality; fill-rule:evenodd; clip-rule:evenodd"
					viewBox="0 0 6396.59 3970.35"
				>
					<g id="Layer_x0020_1">
						<path
							class="fil0"
							d="M4370.84 701.36c310.77,0 603.25,78.25 858.89,216.04 8.2,-10.7 16.51,-21.29 24.92,-31.81 -262.69,-142.85 -563.77,-224.01 -883.81,-224.01 -321.71,0 -624.24,82.05 -887.89,226.29 8.38,10.49 16.64,21.07 24.79,31.75 256.63,-139.19 550.63,-218.26 863.1,-218.26zm-2339.2 -464.22c104.84,0 207.6,8.91 307.57,26.01l0 -0.56c438.64,76.78 823.12,310.98 1093.07,642.22 11.6,-6.78 23.24,-13.48 35,-20.01 -258.66,-319.66 -621.36,-551.67 -1036.6,-644.53l0 0.19c-128.52,-28.22 -262.04,-43.1 -399.04,-43.1 -321.71,0 -624.24,82.05 -887.89,226.29 8.38,10.49 16.64,21.07 24.79,31.75 256.63,-139.19 550.63,-218.26 863.1,-218.26zm399.04 54.25l0 0.16c-128.36,-29.03 -261.9,-44.36 -399.04,-44.36 -310.19,0 -602.06,78.36 -856.95,216.33 236.02,312.49 376.08,701.5 376.08,1123.3 0,682.83 -366.88,1279.8 -914.19,1605 96.91,118.23 208.51,223.95 332.07,314.31l-17.06 0c-120.27,-89.35 -229.05,-193.27 -323.81,-309.11 -11.59,6.82 -23.25,13.54 -35.01,20.1 86.76,106.83 185.17,203.81 293.31,289.01l-16.47 0c-105.21,-84.07 -201.09,-179.33 -285.89,-283.93 -178.75,98.45 -375.34,168.49 -583.72,203.95l0 -10.49c205.96,-35.25 400.32,-104.45 577.14,-201.61 -8.41,-10.5 -16.72,-21.11 -24.91,-31.79 -169.55,92.37 -355.42,158.57 -552.23,193.02l0 -10.2c194.55,-34.25 378.32,-99.72 546.06,-190.92 -236.83,-312.43 -377.41,-701.83 -377.41,-1124.12 0,-682.96 367.59,-1279.94 915.64,-1604.26 -38.98,-47.75 -80.37,-93.45 -123.96,-136.95l6.8 -7.45c44.31,44.2 86.37,90.66 125.95,139.22 11.6,-6.78 23.24,-13.48 35,-20.01 -42.02,-51.93 -86.8,-101.53 -134.1,-148.62l6.97 -7.63c48.09,47.86 93.6,98.31 136.27,151.14 265.49,-145.58 570.27,-228.43 894.42,-228.43 104.77,0 207.51,8.66 307.57,25.29l0 -0.61c457.25,77.8 857.77,321.96 1137.22,667.97 265.49,-145.58 570.27,-228.43 894.42,-228.43 322.49,0 625.82,81.96 890.34,226.15 279.36,-344.81 679.15,-588.06 1135.4,-665.69l0 10.49c-452.39,77.41 -848.86,318.59 -1126.26,660.31 11.79,6.52 23.48,13.2 35.12,19.96 269.85,-330 653.53,-563.3 1091.14,-639.89l0 10.2c-433.92,76.39 -814.39,307.75 -1082.34,634.84 550.23,323.78 919.59,922 919.59,1606.61 0,423.31 -141.24,813.57 -379.11,1126.38 166.61,90.02 348.94,154.7 541.87,188.66l0 10.2c-195.2,-34.16 -379.62,-99.58 -548.05,-190.77 -8.22,10.69 -16.55,21.3 -24.99,31.8 175.72,95.99 368.67,164.38 573.04,199.35l0 10.49c-206.81,-35.19 -402.03,-104.4 -579.68,-201.68 -84.35,103.71 -179.6,198.2 -284.05,281.66l-16.46 0c107.37,-84.59 205.16,-180.8 291.47,-286.74 -11.77,-6.55 -23.49,-13.2 -35.11,-19.98 -94.3,114.87 -202.43,217.98 -321.87,306.71l-17.06 0c122.73,-89.74 233.65,-194.65 330.1,-311.92 -549.49,-324.67 -918.12,-922.91 -918.12,-1607.39 0,-422.8 140.7,-812.67 377.73,-1125.54 -253.89,-136.56 -544.23,-214.09 -852.7,-214.09 -310.19,0 -602.06,78.36 -856.95,216.33 236.02,312.49 376.08,701.5 376.08,1123.3 0,682.83 -366.88,1279.8 -914.19,1605 96.91,118.23 208.51,223.95 332.07,314.31l-17.06 0c-120.27,-89.35 -229.05,-193.27 -323.81,-309.11 -11.59,6.82 -23.25,13.54 -35.01,20.1 86.76,106.83 185.17,203.81 293.31,289.01l-16.47 0c-105.21,-84.07 -201.09,-179.33 -285.89,-283.93 -178.75,98.45 -375.34,168.49 -583.72,203.95l0 -10.49c205.96,-35.25 400.32,-104.45 577.14,-201.61 -8.41,-10.5 -16.72,-21.11 -24.91,-31.79 -169.55,92.37 -355.42,158.57 -552.23,193.02l0 -10.2c194.55,-34.25 378.32,-99.72 546.06,-190.92 -236.83,-312.43 -377.41,-701.83 -377.41,-1124.12 0,-682.96 367.59,-1279.94 915.64,-1604.26 -249.09,-305.11 -595.95,-527.24 -992.81,-618.59zm-1331.06 157.34c8.39,10.43 16.68,20.93 24.83,31.55 11.58,-6.71 23.21,-13.34 34.95,-19.79 -8.15,-10.67 -16.42,-21.24 -24.8,-31.71 -11.75,6.52 -23.39,13.2 -34.98,19.96zm30.96 39.6c232.13,305.01 370.01,685.62 370.01,1098.5 0,666.95 -359.64,1249.8 -895.52,1565.47 8.19,10.57 16.47,21.06 24.89,31.45 545.02,-323.22 910.47,-917.31 910.47,-1596.92 0,-420 -139.63,-807.3 -374.89,-1118.26 -11.75,6.45 -23.38,13.07 -34.96,19.76zm-534.24 2669.15c-11.57,6.74 -23.22,13.36 -34.96,19.83 8.17,10.64 16.45,21.19 24.84,31.65 11.75,-6.54 23.39,-13.24 34.96,-20.03 -8.39,-10.39 -16.67,-20.88 -24.84,-31.44zm-41.12 11.75c11.75,-6.45 23.39,-13.05 34.96,-19.77 -232.99,-304.96 -371.43,-686.01 -371.43,-1099.42 0,-667.06 360.35,-1249.86 896.94,-1564.65 -8.16,-10.59 -16.44,-21.09 -24.83,-31.5 -545.74,322.35 -911.89,916.43 -911.89,1596.16 0,420.52 140.16,808.26 376.25,1119.19zm43.68 -24.95c533.5,-313.77 891.62,-893.75 891.62,-1557.44 0,-411.03 -137.41,-789.92 -368.71,-1093.4 -534.19,312.9 -893.01,892.8 -893.01,1556.6 0,411.55 137.96,790.82 370.09,1094.24zm5240.46 499.52c-11.77,-6.46 -23.45,-13.03 -35.06,-19.74 -8.21,10.58 -16.52,21.08 -24.96,31.48 11.61,6.76 23.32,13.39 35.09,19.92 8.42,-10.46 16.73,-21.02 24.93,-31.66zm-43.81 -24.89c-538.11,-315.12 -899.55,-899.24 -899.55,-1567.86 0,-413.96 138.61,-795.49 371.84,-1100.89 -11.62,-6.68 -23.28,-13.27 -35.06,-19.7 -236.31,311.35 -376.62,699.55 -376.62,1120.59 0,681.26 367.21,1276.62 914.42,1599.3 8.44,-10.38 16.76,-20.87 24.97,-31.44zm-521.59 -2676.81c8.18,-10.59 16.47,-21.1 24.89,-31.51 -11.61,-6.74 -23.28,-13.39 -35.05,-19.88 -8.38,10.47 -16.69,21.02 -24.86,31.68 11.77,6.43 23.42,13.03 35.03,19.71zm33.66 -26.39c-8.41,10.39 -16.71,20.89 -24.89,31.47 538.84,314.23 901,898.32 901,1567.07 0,414.47 -139.16,796.4 -373.22,1101.75 11.6,6.69 23.28,13.25 35.05,19.69 237.12,-311.31 377.96,-699.91 377.96,-1121.45 0,-681.39 -367.94,-1276.74 -915.89,-1598.54zm-31.01 39.52c-232.4,303.89 -370.55,683.69 -370.55,1095.82 0,665.38 359.92,1246.63 895.66,1559.85 233.25,-303.82 371.95,-684 371.95,-1096.65 0,-665.49 -360.62,-1246.68 -897.07,-1559.02zm-1837.79 -42.28c8.39,10.43 16.68,20.93 24.83,31.55 11.58,-6.71 23.21,-13.34 34.95,-19.79 -8.15,-10.67 -16.42,-21.24 -24.8,-31.71 -11.75,6.52 -23.39,13.2 -34.98,19.96zm30.96 39.6c232.13,305.01 370.01,685.62 370.01,1098.5 0,666.95 -359.64,1249.8 -895.52,1565.47 8.19,10.57 16.47,21.06 24.89,31.45 545.02,-323.22 910.47,-917.31 910.47,-1596.92 0,-420 -139.63,-807.3 -374.89,-1118.26 -11.75,6.45 -23.38,13.07 -34.96,19.76zm-534.24 2669.15c-11.57,6.74 -23.22,13.36 -34.96,19.83 8.17,10.64 16.45,21.19 24.84,31.65 11.75,-6.54 23.39,-13.24 34.96,-20.03 -8.39,-10.39 -16.67,-20.88 -24.84,-31.44zm-41.12 11.75c11.75,-6.45 23.39,-13.05 34.96,-19.77 -232.99,-304.96 -371.43,-686.01 -371.43,-1099.42 0,-667.06 360.35,-1249.86 896.94,-1564.65 -8.16,-10.59 -16.44,-21.09 -24.83,-31.5 -545.74,322.35 -911.89,916.43 -911.89,1596.16 0,420.52 140.16,808.26 376.25,1119.19zm43.68 -24.95c533.5,-313.77 891.62,-893.75 891.62,-1557.44 0,-411.03 -137.41,-789.92 -368.71,-1093.4 -534.19,312.9 -893.01,892.8 -893.01,1556.6 0,411.55 137.96,790.82 370.09,1094.24z"
						/>
						<g>
							<path
								class="rotation"
								d="M5308.07 3520.66c-309.46,178.67 -648.5,259.69 -981.45,252.62 0.8,-3.45 1.47,-6.94 2.01,-10.44 330.52,6.71 667.02,-73.88 974.2,-251.23 306.77,-177.11 544.54,-427.8 704.01,-716.87 3.32,1.26 6.68,2.4 10.08,3.42 -160.36,291.38 -399.8,544.08 -708.86,722.51zm137.13 -3293.74c78.72,0 142.53,63.81 142.53,142.54 0,24 -5.94,46.61 -16.42,66.46 166.85,138.72 312.46,308.74 427.3,507.64 291.81,505.42 323.1,1089.73 135.65,1597.54 39.68,25.3 66,69.71 66,120.26 0,78.72 -63.81,142.53 -142.53,142.53 -78.72,0 -142.53,-63.81 -142.53,-142.53 0,-78.72 63.81,-142.54 142.53,-142.54 6.56,0 13.01,0.45 19.34,1.31 181.47,-491.46 151.2,-1056.96 -131.21,-1546.13 -111.2,-192.6 -252.23,-357.23 -413.83,-491.52 -24.05,18.49 -54.15,29.49 -86.82,29.49 -78.72,0 -142.54,-63.81 -142.54,-142.53 0,-15.68 2.54,-30.77 7.22,-44.88 -550.9,-332.6 -1261.21,-363.31 -1857.92,-18.8 -10.35,5.98 -20.61,12.06 -30.8,18.2 -1.1,-3.28 -2.32,-6.5 -3.65,-9.67 9.72,-5.85 19.5,-11.65 29.37,-17.35 599.44,-346.09 1312.88,-315.6 1866.63,17.92 5.29,-12.77 12.39,-24.59 20.97,-35.17l-0.42 0.52c-565.85,-340.68 -1294.82,-371.78 -1907.32,-18.16 -10.06,5.81 -20.02,11.72 -29.93,17.68 19.86,24.5 31.77,55.7 31.77,89.7 0,78.72 -63.82,142.53 -142.54,142.53 -33.56,0 -64.42,-11.6 -88.77,-31.02 0.42,0.34 0.85,0.67 1.27,1 -519.11,429.91 -752.86,1109.62 -625.57,1757.02 -1.01,-0.02 -2.02,-0.03 -3.02,-0.03 16.2,-0.01 32.68,2.77 48.79,8.63 73.97,26.92 112.11,108.72 85.19,182.68 -11.3,31.04 -32.27,55.77 -58.25,72.03l0.03 -0.02c36.39,101.33 82.28,200.85 138.02,297.38 282.24,488.84 756.42,797.71 1272.38,886.51 21.43,-51.62 72.31,-87.93 131.69,-87.93 68.99,0 126.52,49.01 139.7,114.11 322.31,6.91 650.54,-71.5 950.13,-244.46 299.09,-172.67 530.79,-417.22 685.98,-699.2 2.6,2.28 5.27,4.46 8.01,6.53 -156.05,282.87 -388.72,528.18 -688.9,701.49 -300.67,173.59 -630.03,252.45 -953.54,245.84 0.77,5.97 1.16,12.06 1.16,18.23 0,78.72 -63.81,142.53 -142.53,142.53 -78.72,0 -142.54,-63.81 -142.54,-142.53 0,-15.7 2.55,-30.8 7.23,-44.92 -518.1,-89.72 -994.12,-400.14 -1277.58,-891.11 -55.72,-96.52 -101.69,-196 -138.18,-297.29 0.74,-0.39 1.47,-0.79 2.2,-1.19 -12.52,6.91 -26.04,11.92 -40.1,14.84 37.29,103.5 84.26,205.15 141.2,303.77 289.63,501.65 775.96,818.85 1305.32,910.61 -0.15,3.53 -0.15,7.08 -0.04,10.62 -532.98,-91.87 -1022.78,-411 -1314.34,-916 -57.58,-99.74 -105,-202.55 -142.6,-307.24 -21.95,2.87 -44.89,0.66 -67.12,-7.43 -73.97,-26.92 -112.11,-108.71 -85.18,-182.68 14.26,-39.17 43.9,-68.3 79.63,-83.03 -0.83,0.34 -1.66,0.69 -2.49,1.05 -131.55,-668.98 109.96,-1371.36 646.34,-1815.62 0.23,0.44 0.46,0.88 0.69,1.32 -10.67,-19.98 -16.73,-42.8 -16.73,-67.04 0,-78.72 63.81,-142.54 142.53,-142.54 41.55,0 78.94,17.78 104.99,46.14 -0.41,-0.44 -0.81,-0.88 -1.22,-1.31 10.48,-6.32 21.04,-12.58 31.7,-18.73 616.47,-355.92 1350.28,-324.28 1919.5,19.19l-0.11 0.12c26.02,-27.93 63.12,-45.41 104.31,-45.41zm120.81 218.18c-7.19,11.46 -15.96,21.82 -26.01,30.78 161.89,134.82 303.18,299.96 414.66,493.05 283.65,491.3 314.34,1059.19 132.58,1552.97 13.4,2.82 26.1,7.53 37.83,13.83 185.71,-504.59 154.33,-1084.89 -135.53,-1586.93 -113.88,-197.24 -258.19,-365.95 -423.54,-503.69zm-255.5 -122.36c0.16,-0.46 0.32,-0.93 0.49,-1.39 -0.17,0.46 -0.33,0.93 -0.49,1.39zm1.21 -3.35c0.16,-0.42 0.31,-0.83 0.47,-1.24 -0.16,0.41 -0.31,0.83 -0.47,1.24zm133.48 -81.78c72.81,0 131.85,59.03 131.85,131.85 0,72.82 -59.03,131.85 -131.85,131.85 -72.82,0 -131.85,-59.03 -131.85,-131.85 0,-72.82 59.03,-131.85 131.85,-131.85zm-2928.77 2011.84c0.72,-0.29 1.44,-0.58 2.16,-0.86 -0.72,0.28 -1.44,0.57 -2.16,0.86zm3.35 -1.31c0.65,-0.25 1.31,-0.49 1.97,-0.73 -0.66,0.23 -1.32,0.48 -1.97,0.73zm3.31 -1.2c12.66,-4.42 25.98,-7.08 39.56,-7.79 -127.09,-649.87 107.45,-1331.86 627.97,-1763.82 0.44,0.4 0.88,0.79 1.33,1.18 -10.59,-9.32 -19.79,-20.18 -27.24,-32.24l0.09 0.14c-531.91,441.45 -771.57,1138.4 -641.68,1802.51l-0.03 0.01zm39.82 -7.8c1.05,-0.06 2.09,-0.09 3.14,-0.12 -1.05,0.03 -2.09,0.07 -3.14,0.12zm3.55 -0.13c1.01,-0.03 2.02,-0.04 3.03,-0.05 -1.01,0.01 -2.02,0.02 -3.03,0.05zm78.29 263.88c-0.66,0.41 -1.32,0.8 -1.98,1.2 0.66,-0.4 1.32,-0.79 1.98,-1.2zm-2.91 1.74c-0.66,0.39 -1.32,0.77 -1.99,1.14 0.67,-0.38 1.33,-0.76 1.99,-1.14zm-48.54 17.53c-0.44,0.08 -0.87,0.15 -1.31,0.21 0.44,-0.07 0.87,-0.14 1.31,-0.21zm-3.44 0.53c-0.48,0.07 -0.96,0.13 -1.44,0.2 0.48,-0.07 0.96,-0.13 1.44,-0.2zm-143.75 -186.26c24.9,-68.43 100.57,-103.71 169,-78.8 68.42,24.91 103.71,100.57 78.8,169 -24.9,68.43 -100.56,103.71 -169,78.8 -68.42,-24.91 -103.71,-100.57 -78.8,-169zm30.11 10.96c18.85,-51.79 76.13,-78.5 127.92,-59.65 51.79,18.85 78.5,76.12 59.64,127.92 -18.85,51.8 -76.12,78.5 -127.91,59.65 -51.8,-18.85 -78.51,-76.12 -59.65,-127.92zm10.04 3.65c16.83,-46.25 67.98,-70.1 114.23,-53.26 46.25,16.83 70.1,67.98 53.27,114.23 -16.84,46.25 -67.98,70.1 -114.23,53.26 -46.25,-16.83 -70.1,-67.98 -53.26,-114.23zm1701.55 1257.89c72.82,0 131.85,59.03 131.85,131.85 0,72.81 -59.03,131.85 -131.85,131.85 -72.82,0 -131.85,-59.03 -131.85,-131.85 0,-72.82 59.03,-131.85 131.85,-131.85zm0 32.05c55.12,0 99.8,44.68 99.8,99.81 0,55.12 -44.68,99.8 -99.8,99.8 -55.12,0 -99.8,-44.68 -99.8,-99.8 0,-55.12 44.68,-99.81 99.8,-99.81zm0 10.68c49.22,0 89.12,39.9 89.12,89.12 0,49.22 -39.9,89.13 -89.12,89.13 -49.22,0 -89.12,-39.9 -89.12,-89.13 0,-49.22 39.9,-89.12 89.12,-89.12zm1869.93 -1090.11c55.12,0 99.8,44.68 99.8,99.81 0,55.12 -44.68,99.8 -99.8,99.8 -55.12,0 -99.8,-44.68 -99.8,-99.8 0,-55.12 44.68,-99.81 99.8,-99.81zm0 10.68c49.22,0 89.12,39.9 89.12,89.12 0,49.22 -39.9,89.13 -89.12,89.13 -49.22,0 -89.12,-39.9 -89.12,-89.13 0,-49.22 39.9,-89.12 89.12,-89.12zm0 -42.73c72.82,0 131.85,59.03 131.85,131.85 0,72.81 -59.03,131.85 -131.85,131.85 -72.82,0 -131.85,-59.03 -131.85,-131.85 0,-72.82 59.03,-131.85 131.85,-131.85zm-2865.76 -2052.98c0.55,0.48 1.1,0.95 1.65,1.43l-1.65 -1.43zm1.72 1.49c0.52,0.45 1.04,0.88 1.57,1.32 -0.53,-0.44 -1.05,-0.87 -1.57,-1.32zm1.78 1.49c0.48,0.4 0.96,0.79 1.45,1.18 -0.48,-0.39 -0.97,-0.78 -1.45,-1.18zm90.58 -209.85c55.12,0.01 99.81,44.69 99.81,99.81 0,55.12 -44.69,99.8 -99.81,99.8 -55.12,0 -99.8,-44.68 -99.8,-99.8 0,-55.12 44.68,-99.81 99.8,-99.81zm0 10.68c49.22,0.01 89.12,39.9 89.12,89.13 0,49.22 -39.9,89.12 -89.12,89.12 -49.23,0 -89.13,-39.9 -89.13,-89.12 0,-49.22 39.9,-89.13 89.12,-89.13zm106.13 -6.01c0.33,0.37 0.66,0.75 0.99,1.12 -0.33,-0.38 -0.66,-0.75 -0.99,-1.12zm-106.13 -36.71c72.82,0 131.85,59.03 131.85,131.85 0,72.82 -59.03,131.85 -131.85,131.85 -72.82,0 -131.85,-59.03 -131.85,-131.85 0,-72.82 59.03,-131.85 131.85,-131.85zm2159.16 32.04c55.12,0 99.8,44.69 99.8,99.81 0,55.12 -44.68,99.8 -99.8,99.8 -55.12,0 -99.81,-44.68 -99.81,-99.8 0,-55.12 44.69,-99.81 99.81,-99.81zm0 10.68c49.22,0.01 89.12,39.9 89.12,89.13 0,49.22 -39.9,89.12 -89.12,89.12 -49.22,0 -89.12,-39.9 -89.12,-89.12 0,-49.22 39.9,-89.13 89.12,-89.13z"
							/>
						</g>
					</g>
				</svg>
			{/if}
		</div>
	{/if}

	<!-- Banner Icon Below -->
	<div class="overflow">
		<figure>
			{#if type === 'lightcone-event'}
				<div class="bg">
					<img
						class="cone-bg"
						src={$assets[`lc/small/${featured}`]}
						alt={$t(featured)}
						crossorigin="anonymous"
					/>
				</div>
			{/if}

			{#if type === 'starter'}
				<img src={$assets['depature-icon.svg']} alt="Depature" />
			{:else if type === 'regular'}
				<img src={$assets['stellar-icon.svg']} alt="Stellar" />
			{:else if type === 'character-event'}
				<img
					src={$assets[`icon/${featured}`]}
					style={buttonOffset(featured)}
					alt={$t(featured)}
					crossorigin="anonymous"
				/>
			{:else if type === 'lightcone-event'}
				<img
					class="cone-fg"
					src={$assets[`icon/${featured}`]}
					alt={$t(featured)}
					crossorigin="anonymous"
				/>
			{:else if type.match('group')}
				<div class="group">
					{#each content as { featured }, i}
						{#if type.match('cone')}
							<img
								class="cone-fg cone{i}"
								src={$assets[`icon/${featured}`]}
								alt={$t(featured)}
								crossorigin="anonymous"
							/>
						{:else if type.match('character')}
							<div class="group-item">
								<div class="image" style="background-image: url({$assets[`icon/${featured}`]});" />
							</div>
						{/if}
					{/each}
				</div>
			{/if}
		</figure>
	</div>
</button>

<style>
	svg.frame {
		max-width: 100%;
		width: 11.2rem;
		aspect-ratio: 150/60;
		position: relative;
		pointer-events: none;
	}

	:global(.mobileLandscape) svg.frame {
		max-width: 7.2rem;
	}

	.border {
		fill: var(--color-text);
	}

	.svgFill {
		background-color: #40453f;
		aspect-ratio: 160/60.5;
	}

	.svgFill,
	.overflow {
		clip-path: url(#buttonFrame);
		position: absolute;
		left: 1%;
		bottom: 9%;
		width: 97.5%;
		overflow: hidden;
		pointer-events: none;
	}

	:global(.mobileLandscape) .svgFill,
	:global(.mobileLandscape) .overflow {
		bottom: 12.8%;
		left: 1.5%;
	}

	.overflow {
		aspect-ratio: 160/80;
		display: flex;
		justify-content: center;
		align-items: flex-end;
	}

	.overflow figure {
		position: relative;
		bottom: 0;
		display: flex;
		width: 100%;
		aspect-ratio: 160/60;
		overflow: hidden;
	}

	.active .overflow figure {
		overflow: visible;
	}

	.overflow figure::after,
	.overflow figure::before {
		content: '';
		width: 50%;
		height: 100%;
		position: absolute;
		top: 0;
		left: 0;
		z-index: +2;
	}
	.overflow figure::after {
		transform: skew(-20deg) translateX(-20%);
		transition: transform 0.4s ease-in;
	}
	.overflow figure::before {
		transform: skew(-20deg) translateX(-30%);
		transition: transform 0.25s ease-in;
	}

	.active .overflow figure::after {
		background-image: linear-gradient(
			to right,
			rgba(255, 255, 255, 0.2) 30%,
			rgba(255, 255, 255, 0.7)
		);
		transform: skew(-30deg) translateX(220%);
	}

	.active .overflow figure::before {
		background-color: rgba(255, 255, 255, 0.5);
		transform: skew(-30deg) translateX(220%);
	}

	.overflow img {
		position: absolute;
	}

	/* Char Event Button */
	.charevents .overflow img {
		top: -30%;
		width: 110%;
	}

	.group {
		width: 100%;
		height: 100%;
		display: flex;
	}

	.group-item {
		height: 130%;
		width: 100%;
		transform: skew(-20deg) translateY(-20%) translateX(-5%);
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.group-item .image {
		height: 100%;
		aspect-ratio: 16/9;
		transform: skew(20deg);
		background-size: cover;
		background-position: 120% center;
	}

	/* stellar and depature Button */
	.std .overflow img {
		width: 44%;
		right: 17%;
		bottom: 0;
		mask-image: linear-gradient(black 87%, transparent);
	}
	svg.stellar {
		width: 180%;
		position: absolute;
		top: -10%;
		right: -18.5%;
		aspect-ratio: 126.122/78.284;
	}
	svg.stellar path {
		fill: #9b9b9b;
	}

	/* Light Cones Button */
	.bg {
		width: 100%;
		height: 100%;
		background-color: antiquewhite;
		overflow: hidden;
		position: relative;
	}
	img.cone-bg {
		position: absolute;
		right: -15%;
		bottom: -50%;
		width: 300%;
	}

	img.cone-fg {
		width: 55%;
		top: -30%;
		left: 50%;
		transform: translateX(-40%);
	}

	img.cone-fg.cone0 {
		left: 0;
		transform: translateX(0%) translateY(10%) rotate(-40deg) scale(0.9);
		z-index: +2;
	}
	img.cone-fg.cone1 {
		transform: translateX(-50%) translateY(-4%) rotate(-10deg) scale(0.9);
	}

	img.cone-fg.cone2 {
		left: 0;
		transform: translateX(85%) translateY(10%) rotate(10deg) scale(0.9);
		z-index: -1;
	}

	/*  */
	button {
		max-width: 100%;
		position: relative;
		display: inline-block;
		transform: scale(0.9) translateX(-1%);
		transform-origin: left;
		padding-top: 2%;
		filter: brightness(50%);
		transition: transform 0.2s linear 0.23s, filter 0.5s;
	}

	:global(.mobileLandscape) button {
		padding: 0;
		transform: scale(0.92) translateX(-1%);
	}

	button:hover {
		filter: brightness(90%);
	}

	button.active {
		transform: scale(1) translateX(-1%);
		filter: brightness(100%);
	}

	:global(.mobileLandscape) button.active {
		transform: scale(0.97) translateX(3%);
	}

	button.active .rotation {
		animation: rotate infinite linear 30s;
		transform-origin: center;
		transform-box: fill-box;
	}

	button.active::after {
		content: '';
		position: absolute;
		bottom: -3%;
		right: -4%;
		border: 0.1rem solid var(--color-second);
		width: 120%;
		height: 80%;
		z-index: -1;
		opacity: 0.4;
	}

	:global(.mobileLandscape) button.active::after {
		width: 100%;
		bottom: -1%;
		right: -2%;
	}

	/* Mode 2 , button for grouped banner*/
	button.mode2 {
		width: 90%;
		aspect-ratio: 2/0.8;
	}
	button.mode2.active::after {
		display: none;
	}

	.mode2 .svgFill,
	.mode2 .overflow {
		clip-path: none;
	}
	.mode2 .overflow {
		aspect-ratio: 160/65;
		border-bottom: 2.5px solid #fff;
		border-bottom-right-radius: 1rem;
	}
	.mode2 figure {
		aspect-ratio: 160/50;
		border: 2.5px solid #b5a483;
		border-bottom: 0;
	}
	.mode2 figure img {
		margin-top: -4px;
	}

	.ornament {
		opacity: 0;
		position: absolute;
		left: 0;
		top: 50%;
		width: 2px;
		height: 70%;
		background-color: #b5a483;
		transform: translateX(calc(-1 * var(--bw) * 0.026)) translateY(-50%);
		transition: opacity 0.5s;
	}
	.active .ornament {
		opacity: 1;
	}
	.ornament::after {
		content: '';
		width: 2rem;
		border-bottom: 2px dotted #b5a483;
		position: absolute;
		left: 100%;
		top: 50%;
		transform: translateX(45%) translateY(-50%);
	}

	.orb-content {
		position: relative;
		width: 100%;
		height: 100%;
	}

	.circle-right {
		position: absolute;
		top: 50%;
		left: 100%;
		height: 40%;
		transform: translateY(-50%);
		aspect-ratio: 1/1;
		overflow: hidden;
	}
	.circle-right::after {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		border-radius: 100%;
		width: 90%;
		aspect-ratio: 1/1;
		border: 2px dotted #b5a483;
		transform: translateX(-50%);
	}
	.circle-right::before {
		content: '';
		width: 50%;
		aspect-ratio: 1/1;
		background-color: #b5a483;
		position: absolute;
		top: 50%;
		left: 0;
		transform: translateX(-50%) translateY(-50%);
		border-radius: 100%;
	}

	.circle-left {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		right: -100%;
		height: 40%;
		aspect-ratio: 1/1;
	}
	.circle-left::before {
		content: '';
		width: 40%;
		aspect-ratio: 1/1;
		border: 2px solid #b5a483;
		position: absolute;
		top: 50%;
		right: 0;
		transform: translateY(-50%) translateX(15%);
		border-radius: 100%;
	}

	/* Responsive */

	@media screen and (max-width: 750px) {
		button {
			transform-origin: center;
			transform: scale(0.95);
		}
		button.active::after {
			width: 100%;
		}
	}

	@media screen and (max-width: 600px) {
		.svgFill,
		.overflow {
			bottom: 10%;
			left: 1%;
		}
	}

	@keyframes rotate {
		from {
			transform: rotate(0deg);
		}
		to {
			transform: rotate(-360deg);
		}
	}
</style>
