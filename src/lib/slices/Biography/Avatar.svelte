<script lang="ts">
    import {onMount} from "svelte"
	import { type ImageField } from "@prismicio/client";
	import { PrismicImage } from "@prismicio/svelte";
	import clsx from 'clsx';
    import gsap from 'gsap';
	import { components } from "..";

    export let image: ImageField;
    let className: string = "";
    export {className as class};

    let component: HTMLElement;

    onMount(()=>{
        gsap.fromTo('.avatar', {
            opacity: 0,
            scale: 1.4
        },{
            scale: 1,
            opacity: 1,
            duration: 1.3,
            ease: 'power3.inOut'
        }
      );
        
        window.onmousemove = (e) => {
            if (!component) // No component, No animation
            return;
            const componentRect = (component as HTMLElement).getBoundingClientRect();
            const componentCenterX = componentRect.left + componentRect.width / 2;

            let componentPercent = {
                x: (e.clientX - componentCenterX) / componentRect.width / 2
            };
                let distFromCenterX = 1- Math.abs(componentPercent.x)
                
            gsap
                .timeline({   // Animations
                    defaults: {duration:0.5, overwrite: 'auto', ease: 'power3.out'}
                })
                .to('.avatar',{
                    rotation: gsap.utils.clamp(-2, 2, 5 * componentPercent.x)
                })
        };
    });

</script>

<div class={clsx('relative h-full w-full', className)} bind:this={component} >
    <div class="avatar aspect-square overflow-hidden rounded-3xl border-2 border-slate-700 opacity-0 ">
        <PrismicImage 
        field={image} 
        class="avatar-image h-full w-full object-fill" 
        imgixParams={{q:90}}
        />
        
    </div>
</div>

<style>
    .avatar{
        perspective: 500px;
        perspective-origin: 150% 150%;
    }
</style>