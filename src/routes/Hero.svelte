<script>
    import { onMount, onDestroy} from 'svelte';
    import { gsap } from "gsap";
    // import { ScrollTrigger } from "gsap/ScrollTrigger.js";
    import ScrollTriggerPkg from 'gsap/ScrollTrigger.js';
    const { ScrollTrigger } = ScrollTriggerPkg;
    gsap.registerPlugin(ScrollTrigger);

    
    let htfl = ["notes.", "reminders.", "music.", "tasks.", "calendar.", "email.", "plans.", "everything."];
    let hcfl = ["text-emerald-300", "text-green-300", "text-pink-300", "text-violet-300", "text-blue-300", "text-rose-300",  "text-cyan-300", "bg-gradient-to-r from-purple-400 to-blue-400 bg-clip-text text-transparent"]
    let htf = $state(htfl[0]);
    let hcf = $state("text-emerald-300");
    let wordIndex = 0;
    let colorIndex = 0;
    let letterIndex = htfl[0].length;
    let isTyping = false;
    let timeoutId;


    function heroText(){
        let currentWord = htfl[wordIndex];
        let sp = isTyping? 170 : 30;
        

        if(isTyping){
            htf = currentWord.slice(0, letterIndex + 1);
            letterIndex++;
        }else{
            htf = currentWord.slice(0, letterIndex - 1);
            letterIndex--;
        }

        // Now we need to change the word
  
        if(isTyping && letterIndex == currentWord.length){
            isTyping = false;
            timeoutId = setTimeout(heroText, 650);
        }else if(!isTyping && 0 === letterIndex){
            isTyping = true;
            timeoutId = setTimeout(heroText, 200);
            wordIndex = (wordIndex+1) % htfl.length;
            colorIndex++;
            hcf = `${hcfl[colorIndex % hcfl.length]}`;
            console.log(hcf);

        }else{
            timeoutId = setTimeout(heroText, sp);
        }

    }
    

    onMount(() => {
        console.log("on Mount");
        ScrollTrigger.create({
            trigger: "#hero-top",
            start: "top top",
            end: "+=650px",
            pin: true,
            pinSpacing: true,
        });

        timeoutId = setTimeout(heroText, 1000);
        console.log("called function");
        
    })

    onDestroy(() => {
        clearTimeout(timeoutId);
        ScrollTrigger.killAll();
    });

// Idea: have the text do a typewriter effect
    // string.slice(start, end)
    // string - notes note

</script>


<div id="hero-top" class="w-screen">
    <div id="hero-text-main" class=" text-slate-300 self-center w-[440] text-center text-9xl pt-60 pb-15 font-[Lexend] mask font-thin"> <!-- text-center/ mask-radial-from-stone-400 -->
        One place for <br>
        your <span class={hcf}>{htf}</span>
    </div>
    <div id="main-btns" class="w-screen flex justify-center-safe pb-25">
        <button onclick={() => {hcf = "text-blue-300"}} class=" mr-4 cursor-pointer bg-gray-500/30 text-slate-200 h-14 w-fit px-4  text-[24px] border-2 rounded-4xl border-gray-500/30 duration-300">Learn more</button>
        <button onclick={() => {htf = "test"}} class=" ml-4 cursor-pointer duration-150 bg-gray-500/30 text-slate-200 h-14 w-fit px-4 rounded-4xl border-1 border-slate-200 hover:border-slate-400 hover:bg-gray-500/25 text-[25px] ">Join the Waitlist</button>

    </div> 
</div>




<div class="w-screen flex justify-center pb-10">
    <div class=" rounded-[22px] pl-5 pr-5 pt-5 pb-5 bg-gray-300/50 border-gray-300/75 border-1">
        <div class=" bg-gray-900 w-[75vw] h-190 rounded-[17px]" id="sec-1">

        </div>

    </div>
</div>


<div id="fixed-bg1" class="fixed bottom-0 left-0 z-[-20]">
    <img src="/img/bg4.svg" alt="" class="w-screen">
</div>
<div id="fixed-bg2" class="fixed bottom-0 left-0 z-[-23] w-screen h-screen m-0 p-0  to-[#001220] from-[#092a50] bg-linear-0/oklch">
</div>
<div class="hidden">
    <span class="text-blue-300 text-green-300 text-violet-300 text-rose-300 text-orange-300 text-cyan-300 text-amber-300 text-emerald-300 text-pink-300 text-indigo-300 bg-gradient-to-r from-slate-400 via-purple-300 to-blue-400 bg-clip-text text-transparent"></span>
</div>

<style>

</style>