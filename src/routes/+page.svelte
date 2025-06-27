<script>
    import Header from "./Header.svelte";
    import Hero from "./Hero.svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger.js";
    gsap.registerPlugin(ScrollTrigger);
</script>

<Header />
<Hero />

<style>
    :global(body){
        background-color: #001220;
    }
</style>
