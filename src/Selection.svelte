<script>
    export let getSelectionLabel = undefined;
    export let item = undefined;
</script>

 

<div class="overflow-ellipsis overscroll-x-none whitespace-nowrap">
    {@html getSelectionLabel(item)}
</div>
