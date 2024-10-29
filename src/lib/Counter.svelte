<script>
	import { onMount } from "svelte";
	import * as echarts from "echarts";

	function genData() {
		/**
     * 
     *     	动词性	形容词	拟声词	总数
103	52	5	2	162
63.58%	32.10%	3.09%	1.23%	100%
    */

		return [
			{ name: "名词性", value: 103 },
			{ name: "动词性", value: 52 },
			{ name: "形容词", value: 5 },
			{ name: "拟声词", value: 2 },
		];
	}

	function clcikContent() {
		return [
			"打把式 打把势 打白条 打摆子 打苞 打奔儿 打边鼓 打表 打叉 打岔 " +
				"打车 打春 打道 打的 打底子 打点 打点滴 打赌 打盹儿 打趸儿 " +
				"打嗝儿 打更 打工 打钩 打瓜 打卦 打官腔 打官司 打光棍儿 打哈哈 " +
				"打哈欠 打鼾 打寒颤 打寒噤 打寒战 打横 打呼噜 打伙儿 打饥荒 打价 " +
				"打尖1 打尖2 打交道 打醮 打卡 打雷 打擂台 打冷颤 打冷战 打零 " +
				"打马虎眼 打鸣儿 打泡 打炮 打喷嚏 打平手 打谱 打气 打千 打前站 " +
				"打枪1 打枪2 打秋风 打趣 打圈圈 打圈子 打拳 打闪 打扇 打食1 " +
				"打食2 打水漂儿 打胎 打太极拳  打挺儿 打头1 打头2 打头3 打头炮 打头阵 " +
				"打问号 打下手 打先锋 打小儿 打旋 打牙祭 打哑谜 打眼2 打眼3 打样 " +
				"打药 打野外 打夜作 打油 打杂儿 打照面儿 打折 打折扣 打皱 打主意 " +
				"打转转 打总儿 打嘴仗",
			"打扮 打包 打抱不平 打比 打颤 打吵子 打冲锋 打抽丰 打出手 打怵 " +
				"打憷 打叠 打动 打发 打拐 打滚儿  打晃儿 打诨 打假 打搅 打劫 打开 " +
				"打瞌睡 打捞 打擂 打愣 打理 打量 打埋伏 打磨 打拼 打前失 打扰 " +
				"打扫 打算 打探 打听 打通关 打问 打问讯 打消 打掩护 打佯儿  打烊 " +
				"打印 打游击 打圆场 打战 打招呼 打住 打转 打坐",
			"打赤膊 打赤脚 打滑 打紧 打蔫儿",
			"打喳喳 打嘟噜",
		];
	}

	const data = genData();

	const contents = clcikContent();

	let content = contents[0];

	const option = {
		title: {
			text: "打",
			subtext: "词性",
			left: "center",
		},
		tooltip: {
			trigger: "item",
			formatter: "{a} <br/>{b} : {c} ({d}%)",
		},
		series: [
			{
				name: "词性",
				type: "pie",
				radius: "55%",
				center: ["50%", "50%"],
				data: data,
				emphasis: {
					itemStyle: {
						shadowBlur: 10,
						shadowOffsetX: 0,
						shadowColor: "rgba(0, 0, 0, 0.5)",
					},
				},
			},
		],
	};

	let chartbox;

	onMount(() => {
		// let chartDom = document.getElementById(`scatterChart3D${index}`);
		let myChart = echarts.init(chartbox, "dark");

		myChart.setOption(option);

		myChart.on("click", function (params) {
			content = contents[params.dataIndex];
		});
	});
</script>

<div class="box">
	<div class="chart-box" bind:this={chartbox}></div>
	<div class="ctnt">{content}</div>
</div>

<style>
	.box {
		width: 600px;
		margin: 60px auto;
	}
	.chart-box {
		width: 600px;
		height: 600px;
	}
	.ctnt {
		background-color: #2c343c;
		text-align: left;
		padding: 12px;
	}
</style>
