
<script>

    import Post from "../../../lib/Post.svelte";
    import CreatePost from "$lib/CreatePost.svelte";
    import { onMount } from "svelte";
    import { pb } from '$lib/pocketbase.js'

    let posts = []

    let unsubscribe = () => {}


    onMount(async () => {
        const records = await pb.collection('posts').getFullList(200 /* batch size */, {
            sort: '-created',
            expand: 'owner'
        });

        posts = records

        // pb.collection('posts').subscribe('*', function (e) {
        //     const user = await pb.collection('users').getOne(e.record.user)
        //     e.record.expand = { user }
        //     posts = [e.record, ...posts]
        // });

        unsubscribe = await pb
            .collection('posts')
            .subscribe('*', async ({ action, record }) => {

                // Fetch associated user
                const owner = await pb.collection('users').getOne(record.owner);
                record.expand = { owner };
                console.log(record)
                posts = [record, ...posts];
                
                
                // posts = posts.filter((m) => m.id !== record.id);
                
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