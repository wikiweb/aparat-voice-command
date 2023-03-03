# aparat-voice-command

This is a JavaScript code that listens to messages in a chat window and performs some actions based on the content of the messages.

## Here's how the code works:

- It first gets the chat window element and sets up some variables for tracking users and messages.
- It then listens for changes in the chat window using the DOMSubtreeModified event.
- When a new message is added to the chat, the code extracts the text of the message, the username of the sender, and the message ID.
- If the message ID has already been processed, the code skips it to avoid duplicating actions.
- The code then extracts the actual username from the username HTML element and formats it.
- If this is the first message from this user, their username is added to the user list and their username color is set to red.
- A welcome message is spoken by the computer's speech synthesis feature.
- If the message is "w" and the username is not already in the joinedList, the username is added to the joinedList.
- The code then checks the message text and plays a specific sound effect based on the content of the message.
- A timerFlag is used to prevent the code from playing sounds too frequently, with a timeout of 60 seconds between sounds.

```
let listEl = document
  .getElementById("chat")
  .getElementsByClassName("simplebar-content")[1];
let joinedList = [];
let userList = [];
let timerFlag = true;
let synth = window.speechSynthesis;
let messages = {};

listEl.addEventListener("DOMSubtreeModified", () => {
  let chat = $(".simplebar-content .message .message__text")
    .last()[0]
    .innerHTML.toLowerCase();

  let userName = $(".simplebar-content .message .message__username").last()[0]
    .innerHTML;
  let id = $(".simplebar-content .message").last()[0].id;
  if (messages[id]) {
    return false;
  }
  messages[id] = true;

  let newNameLength = userName.length;
  newNameLength = newNameLength - 2;
  userName = userName.slice(0, newNameLength);

  let lastEL = $(".simplebar-content .message .message__username").last();

  if (!userList.includes(userName)) {
    userList.push(userName);
    lastEL.css("color", "red"); //رنگ نام کاربری جدیدی که در چت پیام دهد قرمز می شود

    let toSpeak = new SpeechSynthesisUtterance(userName + " Welcome");
    let selectedVoiceName = "Damayanti";
    let voices = synth.getVoices();
    voices.forEach((voice) => {
      if (voice.name === selectedVoiceName) {
        toSpeak.voice = voice;
      }
    });
    synth.speak(toSpeak); //برای غیر فعال کردن پیام خوش آمد گویی
  }

  if (chat == "w" && !joinedList.includes(userName)) {
    joinedList.push(userName);
  }

  if (timerFlag) {
    let mp3;
    switch (chat) {
      case "finish":
        mp3 = "https://www.myinstants.com/media/sounds/finishhim.swf.mp3";
        break;
      case "damn":
        mp3 = "https://www.myinstants.com/media/sounds/friday-damn.mp3";
        break;
      case "myman":
        mp3 = "https://www.myinstants.com/media/sounds/my-man.mp3";
        break;
      case "fpolice":
        mp3 = "https://www.myinstants.com/media/sounds/mix.mp3";
        break;
      case "ohh":
        mp3 = "https://www.myinstants.com/media/sounds/rap.mp3";
        break;
      case "zart":
        mp3 = "https://www.myinstants.com/media/sounds/fart_2.mp3";
        break;
      case "run":
        mp3 =
          "https://www.myinstants.com/media/sounds/run-vine-sound-effect_1.mp3";
        break;
      case "base":
        mp3 = "https://www.myinstants.com/media/sounds/tmps2cq043x.mp3";
        break;
      case "chekhabare":
        mp3 = "https://www.myinstants.com/media/sounds/ab1_dvZtT8A.mp3";
        break;
      case "gadaye":
        mp3 =
          "https://www.myinstants.com/media/sounds/audio_75a0e05e9824d0506d029963eb2276e0.mp3";
        break;
      case "adam":
        mp3 = "https://www.myinstants.com/media/sounds/emame-rahel.mp3";
        break;
      case "crona":
        mp3 =
          "https://www.myinstants.com/media/sounds/whatsapp-video-2020-03-11-at-19.mp3";
        break;
      case "doornandaz":
        mp3 = "https://www.myinstants.com/media/sounds/tmp8qnikvzw.mp3";
        break;
      case "harmanam":
        mp3 =
          "https://www.myinstants.com/media/sounds/harmanim-baba-nerde-carsafim-full-versiyon-audiotrimmer.mp3";
        break;
      case "sosmast":
        mp3 = "https://www.myinstants.com/media/sounds/susmazbgl1scix-1.mp3";
        break;
      case "fbi":
        mp3 =
          "https://www.myinstants.com/media/sounds/fbi-open-up-sfx_oNGglvo.mp3";
        break;
      case "kekw":
        mp3 = "https://www.myinstants.com/media/sounds/y2mate_jslrh4V.mp3";
        break;
      case "gg":
        mp3 = "https://www.myinstants.com/media/sounds/gg.mp3";
        break;
      case "joonedel":
        mp3 = "https://www.myinstants.com/media/sounds/joonedel-mp3cut.mp3";
        break;
      case "alarm":
        mp3 = "https://www.myinstants.com/media/sounds/alarm.MP3";
        break;
    }

    if (mp3 && timerFlag) {
      timerFlag = false;
      setTimeout(() => {
        timerFlag = true;
      }, 60000); //زمان مورد نیاز تا دستور بعدی به میلی ثانیه
      new Audio(mp3).play();
    }
  }
});

```
