## Overview

These are nodes with generic effector functions that can be used with the Web Audio API.

These nodes can be created and connected in the same way as standard nodes defined by the specification of Web Audio API. The parameters of each node are similar to effector equipment, and you can also modulate it by connecting a signal here

## Usage

* Load `webaudio-macronodes.js` in your HTML.

```html
<script src="https://g200kg.github.io/webaudio-macronodes/webaudio-macronodes.js"></script>
```
* Use defined nodes in web-audio-api program (nodes should be created with constructor (not auciocontext factory method).

  * for Example :  
    `overdrive = new Macro_OverDriveNode(audioctx);`

* For options, you can specify an object that defines the value of each parameter.  
For example, you can set arbitrary initial value by creating Macro_ToneControlNode as follows.
  * `tone = new Macro_ToneControlNode(audioctx, {bass:3, mid:0, treble:-6});`

* After node creation, you can use the node by connecting with the connect() method like ordinary nodes. AudioParam parameters can be controlled automation by automation functions such as setValueAtTime(), also signals from other nodes can be connected.

Example:
```js
...
const tonecontrol = new Macro_ToneControlNode(audioctx, {bass:0, mid:0, treble:3});
sourceNode.connect(tonecontrol).connect(audioctx.destination);
...
```

---

## Macro_ToneControlNode
  This is a node of equalizer function of general bass, mid tone, treble.

Constructor : `new Macro_ToneControlNode(audioctx, options)`

| Parameter |  Type        | Range      | Default |  Description     |
|:---------:|:------------:|:----------:|:-------:|------------------|
| bass      | AudioParam   | [-20..20]  | 0       | gain (dB)        |
| mid       | AudioParam   | [-20..20]  | 0       | gain (dB)        |
| treble    | AudioParam   | [-20..20]  | 0       | gain (dB)        |
| effect    | boolean      | true/false | true    | effect / bypass  |

### Functions
 * getFrequencyResponse(freq, mag, phase)  
 Get frequency response same as  
  `getFrequencyResponse()` of `BiquadFilterNode`

### sample [test-tonecontrol.html](https://g200kg.github.io/webaudio-macronodes/test-tonecontrol.html)

---

## Macro_GraphicEqNode
  This is a node for 7 band graphic equalizer function. The eq parameter is an array of length 7 of AudioParam type.

Constructor : `new Macro_GraphicEqNode(audioctx, options)`

| Parameter |  Type        | Range      | Default |  Description     |
|:---------:|:------------:|:----------:|:-------:|------------------|
| eq[]      | AudioParam[] | [-20..20]  | 0       | gain (dB)        |
| effect    | boolean      | true/false | true    | effect / bypass  |

### Functions
 * getFrequencyResponse(freq, mag, phase)  
 Get frequency response same as  
  `getFrequencyResponse()` of `BiquadFilterNode`

### sample [test-graphiceq.html](https://g200kg.github.io/webaudio-macronodes/test-graphiceq.html)

---

## Macro_ChorusNode
  This is the "chorus effect" node. This node gives a spread to the input sound.

Constructor : `new Macro_ChorusNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description         |
|:---------:|:----------:|:----------:|:-------:|----------------------|
| rate      | AudioParam | [0..10]    | 4       | modulation speed (Hz)|
| depth     | AudioParam | [0..1]     | 0.5     | effect depth         |
| effect    | boolean    | true/false | true    | effect / bypass      |

### sample [test-chorus.html](https://g200kg.github.io/webaudio-macronodes/test-chorus.html)

---

## Macro_PhaserNode
  Phaser effect. 4-stage phaser in the general explanation.

Constructor : `new Macro_PhaserNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description         |
|:---------:|:----------:|:----------:|:-------:|----------------------|
| rate      | AudioParam | [0..10]    | 4       | modulation speed (Hz)|
| depth     | AudioParam | [0..1]     | 0.5     | effect depth         |
| effect    | boolean    | true/false | true    | effect / bypass      |

### sample [test-phaser.html](https://g200kg.github.io/webaudio-macronodes/test-phaser.html)

---

## Macro_DeepPhaserNode
  6-stage phaser effect with resonace control.

Constructor : `new Macro_DeepPhaserNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description         |
|:---------:|:----------:|:----------:|:-------:|----------------------|
| rate      | AudioParam | [0..10]    | 4       | modulation speed (Hz)|
| depth     | AudioParam | [0..1]     | 0.5     | effect depth         |
| resonance | AudioParam | [0..1]     | 0.5     | resonance            |
| effect    | boolean    | true/false | true    | effect / bypass      |

### sample [test-deepphaser.html](https://g200kg.github.io/webaudio-macronodes/test-deepphaser.html)

---

## Macro_DelayNode
  Delay effect with feedback & mixing

| Parameter |  Type      | Range      | Default |  Description     |
|:---------:|:----------:|:----------:|:-------:|------------------|
| delayTime | AudioParam | [0..1]     | 0.5     | delay time (sec) |
| feedback  | AudioParam | [0..1]     | 0.5     | feedback ratio   |
| mix       | AudioParam | [0..1]     | 0.5     | wet mix level    |
| effect    | boolean    | true/false | true    | effect / bypass  |

### sample [test-delay.html](https://g200kg.github.io/webaudio-macronodes/test-delay.html)

---

## Macro_PingPongDelayNode
  Stereo pingpong delay effect. Delayed sound alternates from left and right channels

Constructor : `new Macro_PingPongDelayNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description     |
|:---------:|:----------:|:----------:|:-------:|------------------|
| delayTime | AudioParam | [0..1]     | 0.5     | delay time (sec) |
| feedback  | AudioParam | [0..1]     | 0.5     | feedback ratio   |
| mix       | AudioParam | [0..1]     | 0.5     | wet mix level    |
| effect    | boolean    | true/false | true    | effect / bypass  |

### sample [test-pingpongdelay.html](https://g200kg.github.io/webaudio-macronodes/test-pingpongdelay.html)

---

## Macro_BitCrusherNode
  This is a bit crusher node. This node reduces the number of bits of the signal and creates a Lo-Fi sound.

Constructor : `new Macro_BitCrusherNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description     |
|:---------:|:----------:|:----------:|:-------:|------------------|
| bits      | AudioParam | [1..8]     | 4       | bits             |
| effect    | boolean    | true/false | true    | effect / bypass  |

### sample [test-bitcrusher.html](https://g200kg.github.io/webaudio-macronodes/test-bitcrusher.html)

---

## Macro_OverDriveNode
  This effect generates distortion by soft clipping of the input signal.

Constructor : `new Macro_OverDriveNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description     |
|:---------:|:----------:|:----------:|:-------:|------------------|
| drive     | AudioParam | [0..1]     | 0.5     | drive level      |
| level     | AudioParam | [0..1]     | 0.5     | output level     |
| effect    | boolean    | true/false | true    | effect / bypass  |

### sample [test-overdrive.html](https://g200kg.github.io/webaudio-macronodes/test-overdrive.html)

---

## Macro_FuzzNode
  This effect generates distortion by soft clipping of the input signal.

Constructor : `new Macro_OverDriveNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description     |
|:---------:|:----------:|:----------:|:-------:|------------------|
| fuzz      | AudioParam | [0..1]     | 0.5     | drive level      |
| level     | AudioParam | [0..1]     | 0.5     | output level     |
| effect    | boolean    | true/false | true    | effect / bypass  |

### sample [test-fuzz.html](https://g200kg.github.io/webaudio-macronodes/test-fuzz.html)

---

## Macro_AutoWahNode
  The center frequency of the filter moves according to the envelope of the input signal and creates wah effect.

Constructor : `new Macro_AutoWahNode(audioctx, options)`

| Parameter |  Type      | Range      | Default |  Description         |
|:---------:|:----------:|:----------:|:-------:|----------------------|
| frequency | AudioParam | [100..6000]| 300     | base frequency (Hz)  |
| Q         | AudioParam | [0..10]    | 0.5     | filter Q             |
| sense     | AudioParam | [0..6]     | 4       | sweep width (octave) |
| effect    | boolean    | true/false | true    | effect / bypass      |

### sample [test-autowah.html](https://g200kg.github.io/webaudio-macronodes/test-autowah.html)

