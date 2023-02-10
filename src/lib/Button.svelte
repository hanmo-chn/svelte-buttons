<script lang="ts">

    import {createEventDispatcher} from "svelte";

    export let secondary: boolean = false;
    export let disabled: boolean = false;
    export let size: 'big' | 'medium' | 'small' = 'medium';
    export let style: string='';
    let className: string = '';
    export {className as class};

    const dispatch = createEventDispatcher();

    let ignore = false;

    const handleClickEvent = (e) => {
        if (!disabled && !ignore) {
            ignore = true;
            dispatch('click', e);
            setTimeout(()=>{
                ignore = false;
            }, 300);
        }
        e.stopPropagation();
    }

</script>
<a class="button {size} {className}" class:disabled={disabled} class:ignore={ignore}
   class:secondary={secondary} href="javascript:void(0)" {style} on:click={handleClickEvent}><slot/></a>
