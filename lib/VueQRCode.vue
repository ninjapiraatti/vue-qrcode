
<template>
	<div class="qr-container" v-html="qrCode" />
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue"
import QRCode from "qrcode"

const props = defineProps<{
	input: string
}>()

const qrCode = ref()

const GenerateHTMLQR = async function(input: string) {
	let qrPixels = new Uint8Array
	try {
		const qrObject = QRCode.create(input, { errorCorrectionLevel: "H"})
		qrPixels = qrObject.modules.data
	}
	catch(e) {
		console.log("error", e)
	}
	const qrDiv = document.createElement("div")
	const side = Math.sqrt(qrPixels.length)
	for (let i = 0; i < side; i++) {
		const qrRow = document.createElement("div")
		qrRow.className = "qr-row"
		qrDiv.appendChild(qrRow)
		for (let j = 0; j < side; j++) {
			const pixelDiv = document.createElement("div")
			pixelDiv.className = qrPixels[i * side + j] == 1 ? "qr-pixel qr-pixel-black" : "qr-pixel qr-pixel-white"
			qrRow.appendChild(pixelDiv)
		}
	}
	qrCode.value = qrDiv.innerHTML
}

onMounted(() => {
	GenerateHTMLQR(props.input)
})

</script>

<style scoped>
.qr-container {
	position: absolute;
	right: 20px;
}

.qr-row {
	margin: 0;
	line-height: 0;
	height: 4px;
}

.qr-pixel {
	width: 4px;
	height: 4px;
	display: inline-block;
}

.qr-pixel-black {
	background-color: #000;
}

.qr-pixel-white {
	background-color: #fff;
}
</style>