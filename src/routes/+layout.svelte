<script>
    import "../app.css";
    import { onMount } from "svelte";
    import { goto } from '$app/navigation';
    import { pb } from '$lib/pocketbase.js'
    
    onMount(() => {
      if(pb.authStore.isValid){
        goto('/app/feed')
      } else {
        goto('/login')
      }
    })
</script>



<!-- <h1 class="bg-black">HELLo</h1> -->

<div>

    <slot/>
</div>
