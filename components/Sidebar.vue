<template>
    <div class="offcanvas offcanvas-start" style="width: 300px;" tabindex="-1" id="offcanvasExample" aria-labelledby="offcanvasExampleLabel">
        <div class="offcanvas-header">
            <img src="~/assets/images/logoasdp.png" style="width: 150px;" alt="Logo" class="d-flex justify-content-center">
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <div class="offcanvas-body">
            <ul class="nav nav-pills flex-column mt mt-sm-0">
                <li class="nav-item my-1">
                    <NuxtLink class="nav-link text-black" to="/">
                        <span class="ms-2 d-none d-sm-inline">Dashboard</span>
                    </NuxtLink>
                </li>
                <li class="nav-item my-1">
                    <NuxtLink class="nav-link text-black" to="/kelolaPengguna">
                        <span class="ms-2 d-none d-sm-inline">Kelola Pengguna</span>
                    </NuxtLink>
                </li>
                <li class="nav-item my-1">
                    <NuxtLink class="nav-link text-black" to="/reporting">
                        <span class="ms-2 d-none d-sm-inline">Reporting</span>
                    </NuxtLink>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>

</script>

<style>
.nav-pills li a:hover {
    background-color: rgb(95, 155, 216);
}</style>