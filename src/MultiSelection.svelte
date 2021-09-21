<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    export let value = [];
    export let activeValue = undefined;
    export let isDisabled = false;
    export let multiFullItemClearable = false;
    export let getSelectionLabel = undefined;

    function handleClear(i, event) {
        event.stopPropagation();
        dispatch('multiItemClear', { i });
    }
</script>

<style>
     
   

    .multiSelectItem:hover,
    .multiSelectItem.active {
        background-color: var(--multiItemActiveBG, #006fff);
        color: var(--multiItemActiveColor, #fff);
    }

    .multiSelectItem.disabled:hover {
        background: var(--multiItemDisabledHoverBg, #ebedef);
        color: var(--multiItemDisabledHoverColor, #c1c6cc);
    }

  

    .multiSelectItem_clear:hover,
    .active .multiSelectItem_clear {
        background: var(--multiClearHoverBG, #fff);
    }

    .multiSelectItem_clear:hover svg,
    .active .multiSelectItem_clear svg {
        fill: var(--multiClearHoverFill, #006fff);
    }

    .multiSelectItem_clear svg {
        fill: var(--multiClearFill, #ebedef);
        vertical-align: top;
    }
</style>

{#each value as item, i}
 
    <div class="bg-blue-100 mt-1 ml-1 rounded h-8 flex cursor-default pt-3 pb-4 max-w-full {activeValue === i ? 'active' : ''} {isDisabled ? 'disabled' : ''}" on:click={(event) =>{multiFullItemClearable ? handleClear(i, event) : {}}}>
        <div class="mt-1 overflow-hidden overflow-ellipsis whitespace-nowrap">
            {@html getSelectionLabel(item)}
        </div>
        {#if !isDisabled && !multiFullItemClearable}
            <div
                class="multiSelectItem_clear rounded-2xl bg-blue-200 min-w-full max-w-full h-4 relative top-2 text-center p-1 "
                on:click={(event) => handleClear(i, event)}>
                <svg
                    width="100%"
                    height="100%"
                    viewBox="-2 -2 50 50"
                    focusable="false"
                    aria-hidden="true"
                    role="presentation">
                    <path
                        d="M34.923,37.251L24,26.328L13.077,37.251L9.436,33.61l10.923-10.923L9.436,11.765l3.641-3.641L24,19.047L34.923,8.124 l3.641,3.641L27.641,22.688L38.564,33.61L34.923,37.251z" />
                </svg>
            </div>
        {/if}
    </div>
{/each}
