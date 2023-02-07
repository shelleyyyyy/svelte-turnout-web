<script>
    import { goto } from "$app/navigation";
    import { pb } from "$lib/pocketbase.js"

    const logout = () => {
        pb.authStore.clear()

        goto('/login')
    }
</script>

<div class="navbar bg-base-100">
    <div class="flex-1">
      <a href="/app" class="btn btn-ghost normal-case text-xl">Turnout (JOE IS GAY)</a>
    </div>
    <div class="flex-none gap-2">
        <style>
            import pocketbase
        </style>
      <div class="form-control">
        <input type="text" placeholder="Search" class="input input-bordered" />
      </div>
      <div class="dropdown dropdown-end">
        <label tabindex="0" class="btn btn-ghost btn-circle avatar">
          <div class="w-10 rounded-full">
            <img src="https://upload.wikimedia.org/wikipedia/commons/9/99/Sample_User_Icon.png" />
          </div>
        </label>
        <ul tabindex="0" class="mt-3 p-2 shadow menu menu-compact dropdown-content bg-base-100 rounded-box w-52">
          <li>
          
          </li>
          <li><a href="/app/feed">My Feed</a></li>
          <li><button on:click={logout}>Logout</button></li>
        </ul>
      </div>
    </div>
  </div>