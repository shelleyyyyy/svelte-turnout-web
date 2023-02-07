
<script>

    import Post from "../../../lib/Post.svelte";
    import CreatePost from "$lib/CreatePost.svelte";
    import { onMount } from "svelte";
    import { pb } from '$lib/pocketbase.js'

    let posts = []

    onMount(async () => {
        const records = await pb.collection('posts').getFullList(200 /* batch size */, {
            sort: '-created',
            expand: 'owner'
        });

        posts = records

        console.log(posts)

        pb.collection('posts').subscribe('*', function (e) {
            posts = [e.record, ...posts]
        });
    })

</script>


<div class="grid justify-items-center gap-5 p-5">
    <div class="grid gap-5">
        {#each posts as p}
            <Post title={p.title} description={p.description} tags={p.tags} owner={p.expand.owner.username}/>
        {/each}
    </div>
    <div class="mb-96"></div>
   <div class="fixed bottom-0 bg-base-200 shadow-xl p-5 rounded-lg ">
        <CreatePost/>
   </div>
</div>