# Vue plugin: Vue HTML Qr Code

This is a simple wrapper for generating QR codes in HTML. Semantic versioning only starts from 1.0.10, sorry.

## Installation
```
npm i vue-html-qrcode --save
```

## Usage
In your Vue component, import the plugin:
```ts
import { VueQRCode } from "vue-html-qrcode"

```

And add it to your template:
```html
<VueQRCode
  input="foo"
  fill-color="#000"
  background-color="#fff"
  pixel-size="4px" />

```

### Configuration

| Option | Value type | Default value |
| --- | --- | --- |
| input  | String | Nothing. This value is required. |
| fillColor  | Color for CSS, for example "#000" | "#000" |
| backgroundColor  | Color for CSS, for example "#fff" | "transparent" |
| pixelSize | Size in pixels, for example "1.5px" | "4px" |