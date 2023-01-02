
<template>
	<div class="vue-html-qr-container" v-html="qrCode" />
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue"
import QRCode from "qrcode"

const props = defineProps<{
	input: string,
	fillColor: string,
	backgroundColor: string,
	pixelSize: string
}>()

const defaults = {
	fillColor: "#000",
	backgroundColor: "transparent",
	pixelSize: "4px"
}

const qrCode = ref()

const GenerateHTMLQR = async function(input: string) {
	if (input.length == 0) {
		console.error("No input for QR code")
	}
	let qrPixels = new Uint8Array
	try {
		const qrObject = QRCode.create(input, { errorCorrectionLevel: "H"})
		qrPixels = qrObject.modules.data
	}
	catch(e) {
		console.error("Error creating QR Code:\n", e)
	}
	const qrDiv = document.createElement("div")
	const side = Math.sqrt(qrPixels.length)
	for (let i = 0; i < side; i++) {
		const qrRow = document.createElement("div")
		qrRow.style.height = props.pixelSize || defaults.pixelSize
		qrRow.style.margin = "0"
		qrRow.style.lineHeight = "0"
		qrRow.className = "qr-row"
		qrDiv.appendChild(qrRow)
		for (let j = 0; j < side; j++) {
			const pixelDiv = document.createElement("div")
			pixelDiv.style.width = props.pixelSize || defaults.pixelSize
			pixelDiv.style.height = props.pixelSize || defaults.pixelSize
			pixelDiv.style.display = "inline-block"
			if (qrPixels[i * side + j] == 1) {
				pixelDiv.style.backgroundColor = props.fillColor || defaults.fillColor
			} else {
				pixelDiv.style.backgroundColor = props.backgroundColor || defaults.backgroundColor
			}
			pixelDiv.className = "qr-pixel"
			qrRow.appendChild(pixelDiv)
		}
	}
	qrCode.value = qrDiv.innerHTML
}

onMounted(() => {
	GenerateHTMLQR(props.input)
})

</script>