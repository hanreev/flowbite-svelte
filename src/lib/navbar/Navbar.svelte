<script lang="ts">
  import { twMerge } from "tailwind-merge";
  import clsx from "clsx";
  import { setContext } from "svelte";
  import NavContainer from "./NavContainer.svelte";
  import { navbar } from "./theme";
  import type { NavbarState, NavbarProps } from "$lib/types";

  // propagate props type from underlying Frame

  let { children, fluid, navContainerClass, class: className, ...restProps }: NavbarProps = $props();

  let navState = $state({ hidden: true });
  setContext<NavbarState>("navState", navState);

  let toggle = () => {
    navState.hidden = !navState.hidden;
  };
</script>

<nav>
  <div {...restProps} class={twMerge(navbar(), clsx(className))}>
    <NavContainer {fluid} class={clsx(navContainerClass)}>
      {@render children({ hidden: navState.hidden, toggle, NavContainer })}
    </NavContainer>
  </div>
</nav>

<!--
@component
[Go to docs](https://flowbite-svelte.com/)
## Type
[NavbarProps](https://github.com/themesberg/flowbite-svelte/blob/main/src/lib/types.ts#L1122)
## Props
@prop children
@prop fluid
@prop navContainerClass
@prop class: className
@prop ...restProps
-->
