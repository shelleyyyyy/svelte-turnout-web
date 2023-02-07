
<script>

    import { pb, currentUser } from '$lib/pocketbase.js'


    let title = ""
    let description = ""
    let tags = ""

    const submitPost = async() => {
        const data = {
            "title": title,
            "description": description,
            "tags": [tags],
            "owner": pb.authStore.model?.id
        };

        const record = await pb.collection('posts').create(data);
    }

</script>

<div class=" grid gap-5">

    <div class="flex gap-5">
        <div>
            <h1 class="p-3">Title</h1>
            <input bind:value={title} type="text" placeholder="Title" class="input input-bordered input-success w-full max-w-xs" />
        </div>
    
        <div>
            <h1 class="p-3">Tags</h1>
            <input bind:value={tags} type="text" placeholder="Tags" class="input input-bordered input-success w-full max-w-xs" />
        </div>
        
    </div>

    <div>
        <h1 class="p-3">Description</h1>
        <textarea bind:value={description} class="textarea textarea-primary w-full" placeholder="Bio"></textarea>
    </div>

    <div>
        <h1 class="p-3">Description</h1>
        <button class="btn w-full" on:click={submitPost}>Submit</button>
    </div>
</div>