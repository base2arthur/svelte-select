<script>
    export let isActive = false;
    export let isFirst = false;
    export let isHover = false;
    export let isSelectable = false;
    export let getOptionLabel = undefined;
    export let item = undefined;
    export let filterText = '';

    let itemClasses = '';

    $: {
        const classes = [];
        if (isActive) {
            classes.push('active');
        }
        if (isFirst) {
            classes.push('first');
        }
        if (isHover) {
            classes.push('hover');
        }
        if (item.isGroupHeader) {
            classes.push('groupHeader');
        }
        if (item.isGroupItem) {
            classes.push('groupItem');
        }
        if (!isSelectable) {
            classes.push('notSelectable');
        }
        itemClasses = classes.join(' ');
    }
</script>

<style>
   

    .groupHeader {
        text-transform: var(--groupTitleTextTransform, uppercase);
    }

    .groupItem {
        padding-left: var(--groupItemPaddingLeft, 40px);
    }

    .item:active {
        background: var(--itemActiveBackground, #b9daff);
    }

    .item.active {
        background: var(--itemIsActiveBG, #007aff);
        color: var(--itemIsActiveColor, #fff);
    }

   .item.notSelectable {
        color: var(--itemIsNotSelectableColor, #999);
    }

    .item.first {
        border-radius: var(--itemFirstBorderRadius, 4px 4px 0 0);
    }

    .item.hover:not(.active) {
        background: var(--itemHoverBG, #e7f2ff);
        color: var(--itemHoverColor, inherit);
    }
</style>
 
<div class="item cursor-default h-11 pb-5 overflow-ellipsis whitespace-nowrap hover:text-gray-300  {itemClasses}">
    {@html getOptionLabel(item, filterText)}
</div>
