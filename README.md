# aparat-voice-command


```
var listEl = document.getElementById('chat').getElementsByClassName('simplebar-content')[0];
var joinedList = []
var userList = []
var timerFlag = true;
var synth = window.speechSynthesis;
var messages= {};

listEl.addEventListener('DOMSubtreeModified',function(){

    var chat = $('.simplebar-content .message .message__text').last()[0].innerHTML.toLowerCase();
    var userName= $('.simplebar-content .message .message__username').last()[0].innerHTML;
    var id = $('.simplebar-content .message').last()[0].id;
    var badgeElm = $($('.simplebar-content .message').last()[0]).find('.message__badge')[0]

    if(messages[id]){
        return false;        
    }
    messages[id] = true;
    
    var newNameLength = userName.length
    newNameLength = newNameLength-2
    userName = userName.slice(0,newNameLength)

    let lastEL = $('.simplebar-content .message .message__username').last()


    if(!userList.includes(userName)){ 
        userList.push(userName)
        lastEL.css('color','red') //رنگ نام کاربری جدیدی که در چت پیام دهد قرمز می شود

        var toSpeak = new SpeechSynthesisUtterance(userName + ' Welcome'); 
            var selectedVoiceName = "Damayanti";
            var voices = synth.getVoices();
            voices.forEach((voice)=>{
                if(voice.name === selectedVoiceName){
                    toSpeak.voice = voice; 
                }
            });
            synth.speak(toSpeak); //برای غیر فعال کردن پیام خوش آمد گویی
    }


    if(chat == 'w' && !joinedList.includes(userName)){
        joinedList.push(userName)
    }


    if(badgeElm !== undefined){
        if(timerFlag){
             var mp3
             switch(chat) {
                case  "finish":
                     mp3 = "https://www.myinstants.com/media/sounds/finishhim.swf.mp3";
                     break;
                case  "damn":
                     mp3 = "https://www.myinstants.com/media/sounds/friday-damn.mp3";
                     break;
                case  "myman":
                     mp3 = "https://www.myinstants.com/media/sounds/my-man.mp3";
                     break;
                case  "fpolice":
                     mp3 = "https://www.myinstants.com/media/sounds/mix.mp3";
                     break;
                case  "ohh":
                     mp3 = "https://www.myinstants.com/media/sounds/rap.mp3";
                     break;
                case  "zart":
                     mp3 = "https://www.myinstants.com/media/sounds/fart_2.mp3";
                     break;                
                case  "run":
                     mp3 = "https://www.myinstants.com/media/sounds/run-vine-sound-effect_1.mp3";
                     break;                
                case  "base":
                     mp3 = "https://www.myinstants.com/media/sounds/tmps2cq043x.mp3";
                     break;                
                case  "chekhabare":
                     mp3 = "https://www.myinstants.com/media/sounds/ab1_dvZtT8A.mp3";
                     break;                
                case  "gadaye":
                     mp3 = "https://www.myinstants.com/media/sounds/audio_75a0e05e9824d0506d029963eb2276e0.mp3";
                     break;                
                case  "adam":
                     mp3 = "https://www.myinstants.com/media/sounds/emame-rahel.mp3";
                     break;                
                case  "crona":
                     mp3 = "https://www.myinstants.com/media/sounds/whatsapp-video-2020-03-11-at-19.mp3";
                     break;     
                case  "doornandaz":
                     mp3 = "https://www.myinstants.com/media/sounds/tmp8qnikvzw.mp3";
                     break;                
               
                case  "harmanam":
                     mp3 = "https://www.myinstants.com/media/sounds/harmanim-baba-nerde-carsafim-full-versiyon-audiotrimmer.mp3";
                     break;                           
                case  "sosmast":
                     mp3 = "https://www.myinstants.com/media/sounds/susmazbgl1scix-1.mp3";
                     break;
                 case "fbi":
                     mp3 = "https://www.myinstants.com/media/sounds/fbi-open-up-sfx_oNGglvo.mp3";
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
 
             if(mp3 && timerFlag){
                 timerFlag = false;
                 setTimeout(()=>{ timerFlag =true },60000) //زمان مورد نیاز تا دستور بعدی به میلی ثانیه
                 new Audio(mp3).play(); 
             }
        }
     }
    
});
```
