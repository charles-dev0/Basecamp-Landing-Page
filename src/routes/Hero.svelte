<script>
    import { onMount } from 'svelte';
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    gsap.registerPlugin(ScrollTrigger);

    onMount(() => {
        gsap.to("#a", {
            x: 400,
            duration: 3,
            rotation: 360,
    }
    );
    })


</script>



<div id="a" class="bg-white w-fit">
    test
</div>