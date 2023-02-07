

<script>

    export let owner;
    export let title;
    export let description;
    export let tags;
    // export let userid;

</script>



<div class="card bg-base-100 w-96 shadow-xl">
    <!-- <figure><img src="https://www.vmi.edu/media/content-assets/images/academic-departments/computer-science/cydef/cydef/Corson.jpg" alt="Shoes" /></figure> -->
    <div class="card-body">
        <h2 class="card-title">
            {title} | {owner}
            <!-- <div class="badge badge-secondary">NEW</div> -->
        </h2>
        <p>{description}</p>
        <div class="card-actions justify-end">
            <div class="badge badge-outline">{tags}</div> 
            <div class="badge badge-outline">Products</div>
        </div>
    </div>
</div>