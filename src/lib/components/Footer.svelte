<script lang="ts">
	import { type Content, isFilled } from "@prismicio/client";
	import { PrismicLink } from "@prismicio/svelte";
  import IconGithub from '~icons/fa-brands/github';
  import IconLinkedin from '~icons/fa-brands/linkedin';
  import Bounded from "./Bounded.svelte";

    export let Settings: Content.SettingsDocument;
</script>

<Bounded as="footer" class="text-slate-600">

  <div class="container mx-auto flex mt-20 flex-col items-center justify-between gap-6 py-8 sm:flex-row">
    <div class="name flex flex-col items-center justify-center gap-x-4 gap-y-2 sm:flex-row sm:justify-self-start">
        <a
          href="/" class="text-xl font-extrabold tracking-tighter text-slate-100 transition-color duration-150 hover:text-yellow-400">
          {Settings.data.name = "Portfolio"}
        </a>

        <span class="hidden text-5xl font-extralight leading-[0] text-slate-400 sm:inline" aria-hidden="true"
        >/</span>
        <p class="text-sm text-slate-300">
            © {new Date().getFullYear()} 
            {Settings.data.name = "DevX"}
        </p>
    </div>
    <nav class="navigation" aria-label="Footer Navigation">
        <ul class="flex items-center gap-1">
          {#each Settings.data.nav_item as {link, label}, index}
            <li>
                <PrismicLink field={link} class="block px-3 py-1 text-base font-bold text-slate-100 transition-colors duration-150 hover:text-yellow-400">{label}</PrismicLink>
            </li>
            {#if index < Settings.data.nav_item.length -1}
              <span class="text-4xl font-thin leading-[0] text-slate-400" aria-hidden="true" >
                /
              </span>
            {/if}
          {/each}
        </ul>
    </nav>

    <div class="socials inline-flex justify-center sm:justify-end ">
        {#if isFilled.link(Settings.data.github_link)}
        <PrismicLink 
            field={Settings.data.github_link} class="p-2 text-2xl text-slate-300 translate-all duration-150 hover:scale-125 hover:text-yellow-400"
            aria-label={ Settings.data.name + 'on Github' }
        >
           <IconGithub />
        </PrismicLink>
        {/if}

        {#if isFilled.link(Settings.data.linkedin_link)}
        <PrismicLink 
            field={Settings.data.linkedin_link} class="p-2 text-2xl text-slate-300 translate-all duration-150 hover:scale-125 hover:text-yellow-400"
            aria-label={ Settings.data.name + 'on Linkedin' }
        >
           <IconLinkedin />
        </PrismicLink>
        {/if}
    </div>
  </div>

</Bounded>