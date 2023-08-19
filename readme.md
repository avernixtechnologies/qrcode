# Avernix Technologies QRCode

Avernix Technologies QRCode generator is a NodeJS server side javascript QRCode image(PNG/JPEG/SVG/Base64 data url) generator. Support setting Dot style, Logo, Background image, Colorful, Title and more. Support binary(hex) data mode.

Forked from EasyQRCodeJS-NodeJS


## Table of contents

- [Avernix Technologies QRCode](#avernix-technologies-qrcode)
  - [Table of contents](#table-of-contents)
  - [Feature](#feature)
  - [Demo preview](#demo-preview)
  - [QR Code Structure](#qr-code-structure)
  - [Installation](#installation)
  - [Basic Usages](#basic-usages)
  - [QRCode API](#qrcode-api)
    - [Object](#object)
    - [Options](#options)
    - [Methods](#methods)
  - [TypeScript Support](#typescript-support)
  - [License](#license)
  - [End](#end)

## Feature

- **English**

    - Save QRCode image file without DOM on server side

	- Support save PNG/JPEG/SVG image file

	- Support get standard base64 image data url text: `data:image/png;base64, ...`

	- Support get SVG data text: `<svg xmlns:xlink="http://www.w3.org/1999/xlink" ...`

    - Support get a stream from Canvas
    
    - Required Patterns that support dot style
 
    - Support for Quiet Zone settings
	
    - Support custom Position Pattern inner fill and outer border color

    - Support custom Alignment Pattern inner fill and outer border color

    - Support custom Timing Patterns vertical, horizontal color

    - Support Logo images (including transparent PNG images)

    - Support Background Image

    - Support for title, subtitle settings
    
    - Support binary(hex) data mode

    - Support TypeScript
## Demo preview

![Demo preview](doc/images/demo.png)

## QR Code Structure

![QR Code Structure](doc/images/QR_Code_Structure.png)


## Installation

```HTML
npm i @trarn/qrcode
```


## Basic Usages

```JS
const QRCode = require('@trarn/qrcode');

// Options
var options = {
	text: "www.avernix.com"
};

// New instance with options
var qrcode = new QRCode(options);

// Save QRCode image
qrcode.saveImage({
	path: 'q.png' // save path
});
```

## QRCode API

### Object

```JS
var qrcode = new QRCode(options);
```


### Options

```JS
 var options = {
    // ====== Basic
    text: "https://github.com/avernixtechnologies/qrcode",
    width: 256,
    height: 256,
    colorDark : "#000000",
    colorLight : "#ffffff",
    correctLevel : QRCode.CorrectLevel.H, // L, M, Q, H

    // ====== dotScale
    /*
    dotScale: 1, // For body block, must be greater than 0, less than or equal to 1. default is 1

    dotScaleTiming: 1, // Dafault for timing block , must be greater than 0, less than or equal to 1. default is 1
    dotScaleTiming_H: undefined, // For horizontal timing block, must be greater than 0, less than or equal to 1. default is 1
    dotScaleTiming_V: undefined, // For vertical timing block, must be greater than 0, less than or equal to 1. default is 1

    dotScaleA: 1, // Dafault for alignment block, must be greater than 0, less than or equal to 1. default is 1
    dotScaleAO: undefined, // For alignment outer block, must be greater than 0, less than or equal to 1. default is 1
    dotScaleAI: undefined, // For alignment inner block, must be greater than 0, less than or equal to 1. default is 1
    */

    // ====== Quiet Zone
    /*
    quietZone: 0,
    quietZoneColor: "rgba(0,0,0,0)",
    */

    // ====== Logo
    /*
    logo: "../demo/logo.png", // Relative address, relative to `easy.qrcode.min.js`
    logo: "https://avernix.com/images/avernix-technologies-icon.png", 
    logoWidth: 80, // fixed logo width. default is `width/3.5`
    logoHeight: 80, // fixed logo height. default is `heigth/3.5`
    logoMaxWidth: undefined, // Maximum logo width. if set will ignore `logoWidth` value
    logoMaxHeight: undefined, // Maximum logo height. if set will ignore `logoHeight` value
    logoBackgroundColor: '#fffff', // Logo backgroud color, Invalid when `logBgTransparent` is true; default is '#ffffff'
    logoBackgroundTransparent: false, // Whether use transparent image, default is false
    */

    // ====== Backgroud Image
    /*
    backgroundImage: '', // Background Image
    backgroundImageAlpha: 1, // Background image transparency, value between 0 and 1. default is 1. 
    autoColor: false, // Automatic color adjustment(for data block)
    autoColorDark: "rgba(0, 0, 0, .6)", // Automatic color: dark CSS color
    autoColorLight: "rgba(255, 255, 255, .7)", // Automatic color: light CSS color
    */

    // ====== Colorful
    // === Posotion Pattern(Eye) Color
    /*
    PO: '#e1622f', // Global Posotion Outer color. if not set, the defaut is `colorDark`
    PI: '#aa5b71', // Global Posotion Inner color. if not set, the defaut is `colorDark`
    PO_TL:'', // Posotion Outer color - Top Left 
    PI_TL:'', // Posotion Inner color - Top Left 
    PO_TR:'', // Posotion Outer color - Top Right 
    PI_TR:'', // Posotion Inner color - Top Right 
    PO_BL:'', // Posotion Outer color - Bottom Left 
    PI_BL:'', // Posotion Inner color - Bottom Left 
    */
    // === Alignment Color
    /*
    AO: '', // Alignment Outer. if not set, the defaut is `colorDark`
    AI: '', // Alignment Inner. if not set, the defaut is `colorDark`
    */
    // === Timing Pattern Color
    /*
    timing: '#e1622f', // Global Timing color. if not set, the defaut is `colorDark`
    timing_H: '', // Horizontal timing color
    timing_V: '', // Vertical timing color
    */

    // ====== Title
    /*
    title: 'QR Title', // content 
    titleFont: "normal normal bold 18px Arial", //font. default is "bold 16px Arial"
    titleColor: "#004284", // color. default is "#000"
    titleBackgroundColor: "#fff", // background color. default is "#fff"
    titleHeight: 70, // height, including subTitle. default is 0
    titleTop: 25, // draws y coordinates. default is 30
    */

    // ====== SubTitle
    /*
    subTitle: 'QR subTitle', // content
    subTitleFont: "normal normal normal 14px Arial", // font. default is "14px Arial"
    subTitleColor: "#004284", // color. default is "4F4F4F"
    subTitleTop: 40, // draws y coordinates. default is 0
    */

    // ===== Event Handler
    /*
    onRenderingStart: undefined,
    */

    // ==== Images format
    /*
    format: 'PNG', // 'PNG', 'JPG'
    compressionLevel: 6, // ZLIB compression level (0-9). default is 6
    quality: 0.75, // An object specifying the quality (0 to 1). default is 0.75. (JPGs only) 
    */

    // ==== Versions
    /*
    version: 0, // The symbol versions of QR Code range from Version 1 to Version 40. default 0 means automatically choose the closest version based on the text length.
    */     

    // ===== Binary(hex) data mode
    /*
    binary: false, // Whether it is binary mode, default is text mode. 
    */ 

    // =====  UTF-8 without BOM
    /*
    utf8WithoutBOM: true
    */        
}
```

| Option | Required | Type | Defaults | Description |
| --- | --- |--- | --- |--- |
| Basic options| --- | ---|---|---|
| **text** | Y | String |`''` |  Text |
| **width** | N | Number | `256` |  Width | 
| **height** | N | Number | `256` |  Height | 
| **colorDark** | N | String | `#000000` | Dark CSS color | 
| **colorLight** | N | String | `#ffffff` | Light CSS color | 
| **correctLevel** | N | Enum | `QRCode.CorrectLevel.H` | `QRCode.CorrectLevel.H`<br/>`QRCode.CorrectLevel.Q` <br/> `QRCode.CorrectLevel.M` <br/> `QRCode.CorrectLevel.L`| 
| Dot style| --- | ---|---|---|
| **dotScale** | N | Number | `1.0` |Dot style scale. Ranges: `0-1.0` |
| **dotScaleTiming** | N | Number | `1.0` |Dot style scale for timing. Ranges: `0-1.0` |
| **dotScaleTiming_V** | N | Number | `undefined` |Dot style scale for horizontal timing. Ranges: `0-1.0` |
| **dotScaleTiming_H** | N | Number | `undefined` |Dot style scale for vertical timing. Ranges: `0-1.0` |
| **dotScaleA** | N | Number | `1.0` |Dot style scale for alignment. Ranges: `0-1.0` | 
| **dotScaleAO** | N | Number | `undefined` |Dot style scale for alignment outer. Ranges: `0-1.0` |
| **dotScaleAI** | N | Number | `undefined` |Dot style scale for alignment inner. Ranges: `0-1.0` |
| Quiet Zone| --- | ---|---|---|
| **quietZone** | N | Number | `0` |  Quiet Zone size | 
| **quietZoneColor** | N | String | `rgba(0,0,0,0)` |  Background CSS color to Quiet Zone | 
| Logo options| --- | ---|---|---|
| **logo** | N | String | `undefined` | Logo Image Path or Base64 encoded image. If use relative address, relative to `easy.qrcode.min.js` |  
| **logoWidth** | N | Number | `width/3.5` |  Fixed logo width. |
| **logoHeight** | N | Number | `height/3.5` |  fixed logo height. | 
| **logoMaxWidth** | N | Number | `undefined` |  Maximum logo width. if set will ignore `logoWidth` value. | 
| **logoMaxHeight** | N | Number | `undefined` |  Maximum logo height. if set will ignore `logoHeight` value. |  
| **logoBackgroundTransparent** | N | Boolean | `false` |  Whether the background transparent image(`PNG`) shows transparency. When `true`, `logoBackgroundColor` is invalid |  
| **logoBackgroundColor** | N | String | `#ffffff` |  Set Background CSS Color when image background transparent. Valid when `logoBackgroundTransparent` is `false` |  
| Backgroud Image options|  ---|--- |---|---|
| **backgroundImage** | N | String | `undefined` | Background Image Path or Base64 encoded image. If use relative address, relative to `easy.qrcode.min.js` | 
| **backgroundImageAlpha** | N | Number | `1.0` |  Background image transparency. Ranges: `0-1.0`  |  
| **autoColor** | N | Boolean | `false` |  Automatic color adjustment(for data block) | 
| **autoColorDark** | N | String | `rgba(0, 0, 0, .6)` |  Automatic color: dark CSS color  |
| **autoColorLight** | N | String | `rgba(255, 255, 255, .7)` |  Automatic color: light CSS color |
| Posotion Pattern Color options| --- | ---|---|---|
| **PO** | N | String | `undefined` | Global Posotion Outer CSS color. if not set, the defaut is `colorDark` | 
| **PI** | N | String | `undefined` | Global Posotion Inner CSS color. if not set, the defaut is `colorDark` | 
| **PO_TL** | N | String | `undefined` | Posotion Outer CSS color - Top Left |  
| **PI_TL** | N | String | `undefined` | Posotion Inner CSS color - Top Left |  
| **PO_TR** | N | String | `undefined` | Posotion Outer CSS color - Top Right |  
| **PI_TR** | N | String | `undefined` | Posotion Inner CSS color - Top Right | 
| **PO_BL** | N | String | `undefined` | Posotion Outer CSS color - Bottom Left | 
| **PI_BL** | N | String | `undefined` | Posotion Inner CSS color - Bottom Left | 
| Alignment Color options| --- |--- |---|---|
| **AO** | N | String | `undefined` | Alignment Outer CSS color. if not set, the defaut is `colorDark` | 
| **AI** | N | String | `undefined` | Alignment Inner CSS color. if not set, the defaut is `colorDark` |  
| Timing Pattern Color options| --- | ---|---|---|
| **timing** | N | String | `undefined` | Global Timing CSS color. if not set, the defaut is `colorDark` |  
| **timing_H** | N | String | `undefined` | Horizontal timing CSS color |  
| **timing_V** | N | String | `undefined` | Vertical timing CSS color |  
| Title options| --- | ---|---|---|
| **title** | N | String | `''` |  | 
| **titleFont** | N | String | `normal normal bold 16px Arial` | CSS Font |  
| **titleColor** | N | String | `#000000` | CSS color |  
| **titleBackgroundColor** | N | String | `#ffffff` | CSS color| 
| **titleHeight** | N | Number | `0` | Title Height, Include subTitle |  
| **titleTop** | N | Number | `30` | draws y coordinates.| 
| SubTitle options| --- | ---|---|---|
| **subTitle** | N | String | `''` |  |  
| **subTitleFont** | N | String | `normal normal normal 14px Arial` | CSS Font | 
| **subTitleColor** | N | String | `#4F4F4F` | CSS color | 
| **subTitleTop** | N | Number | `0` | draws y coordinates. default is 0|
| Event Handler options| --- | ---|---|---|
| **onRenderingStart(qrCodeOptions)** | N | Function | `undefined` | Callback function when rendering start work. can use to hide loading state or handling.  | 
| Images format options| --- | ---|---|---|
| **format** | N | String | `PNG` | 'PNG' or 'JPG'  |
| **compressionLevel** | N | Number | `6` | ZLIB compression level between 0 and 9. (**PNGs only**)  |
| **quality** | N | Number | `0.75` | An object specifying the quality (0 to 1). (**JPGs only**)  |
| Version options| --- | ---|---|---|
| **version** | N | Number | `0` | The symbol versions of QR Code range from Version `1` to Version `40`. default 0 means automatically choose the closest version based on the text length.  [Information capacity and versions of QR Codes](https://www.qrcode.com/en/about/version.html) **NOTE**: If you set a value less than the minimum version available for text, the minimum version is automatically used. |
| UTF-8 options| --- | ---|---|---|
| **utf8WithoutBOM** | N | Boolean | `true` | Use UTF-8 without BOM. set to `false` value will use BOM in UFT-8.|
| Binary(hex) data model options| --- | ---|---|---|
| **binary** | N | Boolean | `false` | Whether it is binary mode, default is text mode.  | 

    
### Methods

- **saveImage(ImagesFormatOptions)**

	```JS
	//  Save PNG Images to file
	qrcode.saveImage({
		path: 'q.png' // file path
	}).then(data=>{
       console.log("`q-premium1.png` has been Created!");
    });
	```

- **saveSVG(ImagesFormatOptions)**

	```JS
	//  Save SVG to file
	qrcode.saveSVG({
		path: 'qrcode.svg' // file path
	}).then(data=>{
       console.log("`qrcode.svg` has been Created!");
    });
	```
        
- **toDataURL()**
 
	```JS
	// Get standard base64 image data url text: 'data:image/png;base64, ...'
	qrcode.toDataURL().then(data=>{
		console.info('======QRCode PNG Base64 DataURL======')
		console.info(data);
	});
	```
    
- **toSVGText()**
 
	```JS
	// Get SVG data text: '<svg xmlns:xlink="http://www.w3.org/1999/xlink" ...'
	qrcode.toSVGText().then(data=>{
		console.info('======QRCode SVG Data Text======')
		console.info(data)
	});
	```
    
- **toStream()**
 
	```JS
    const out = fs.createWriteStream(`qrcode-stream.png`);
    // const stream = await qrcode.toStream();
    // stream.pipe(out);
    // out.on('finish', () => console.log('Finsihed'));

    qrcode.toStream().then(res=>{
        res.pipe(out).on('finish', () => console.log('Finsihed'));
    })
	```
        
## TypeScript Support

Update to version `3.7.1+`.

```Javascript
import QRCode = require("@trarn/qrcode")
```

## License
MIT License
## End

Email：<kyle@avernix.com>

[http://www.avernix.com](http://www.avernix.com "Avernix Technologies Home")



