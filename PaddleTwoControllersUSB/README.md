# mr.Spinner - Spinner and Paddle USB adapter for MiSTer

## Introduction
It's a simple adapter for 2 independent input devices in a single Arduino Micro (ATmega32U4) board.

### Paddle
For paddle you need a linear potentiometer with 10K-1M resistance and a button. You can use Atari 2600 paddles, but you need to add a simple modification to paddles. **You need to connect unconnected 3rd pin of potentiometer to a black wire of button (ground pin).**

### Spinner
You can use almost any 2-phase spinner. Hight-PPR (300+) spinners provider more smooth scroll while even simple minniature Arduino shield spinner with 20PPR is fine. PPR value includes 4 steps of 2-phase encoder, so 20PPR spinner means 80 steps. This adapter is splitting PPR to steps, so 20PPR spinner gives 80 pulses to the FPGA core. Thus even 20PPR is good enough to play all spinner games. However minniature passive spinners line the one used in Arduino shield has clicking mechanism (one cleak per PPR) which making hard to use it for playing the games. Luckily, you can disassemble such spinner (carefully strighten those 4 V-locks to remove the top part) and flatten the pimple to eliminate the clicks. After this modification you can use 20PPR spinner to play the games.

Standard Atari 2600 driving controller is 4PPR spinner which is not acceptable for using. However you can try to mod it by installing 20-40PPR passive micro spinner inside.

Optical 360-600PPR spinners are supported as well. You just need to provide the 5V power to such spinner.

### Connecting/Assembling
If you use Atari 2600 paddles, then just use standard DB9 connector. If you use driving controller then you will need 2 DB9 sockets.

Connector 1:
| DB9 | Arduino Micro pin | Beetle pin | Function |
| ----- | ------ | ------ | ------ |
| 1 | TXO(1) | TXO(1) | Spinner_A   |
| 2 | RXI(0) | RXI(0) | Spinner_B   |
| 3 | 3      | 10     | Paddle2 Btn |
| 4 | 4      | 11     | Paddle1 Btn |
| 5 | A0     | A0     | Paddle1 Pot |
| 6 | 6      | 9      | Spinner Btn |
| 7 | VCC    | VCC    | VCC         |
| 8 | GND    | GND    | GND         |
| 9 | A1     | A0     | Paddle2 Pot |

Connector 2:
| DB9 | Arduino Micro pin | Beetle pin | Function |
| ----- | ------ | ------ | ------ |
| 1 | 2   | 3   | Spinner_A   |
| 2 | 7   | 2   | Spinner_B   |
| 6 | 15  | 15  | Spinner Btn |
| 7 | VCC | VCC | VCC         |
| 8 | GND | GND | GND         |

### Source parameters
Firmware has several definitions to tweak for best experience:

1. BEETLE: support for miniature board version with USB plug integrated. Enable it if you use Beetle board - it uses other pins.
2. SPINNER_PPR: set the correct PPR value according to your spinner for correct work.
3. PADDLE_EMU: enable paddle emulation by spinner if defined. So bassically the spinner is the only you need for both spinner and paddle control.
4. PADDLE_SUPPORT: support for physical paddles. Even if this option is disabled, the paddle emulation mode by spinner will continue to work.
5. DEV_NUM: set it to 2 or 1. If you integrate the board into some controller's case with only single spinner/paddle, then 1 would be better.

### Dependencies
If PADDLE_SUPPORT is defined, then additional **ResponsiveAnalogRead** library is required. You can install it in library manager function of Arduino IDE.

## License
This project is licensed under the GNU General Public License v3.0.
