<template>
    <div>

        <!-- Navbar -->

        <nav class="navbar navbar-expand-lg bg-body-tertiary shadow"> <!-- pb-2 untuk kebawah dari navbar-->
            <div class="container">
                <a class="btn btn-light me-3" data-bs-toggle="offcanvas" href="#offcanvasExample" role="button"
                    aria-controls="offcanvasExample">
                    <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="currentColor" class="bi bi-list"
                        viewBox="0 0 16 16">
                        <path fill-rule="evenodd"
                            d="M2.5 12a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5m0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5m0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5" />
                    </svg>
                </a>



                <div class="d-flex flex-column align-items-start">
                    <div class="text-capitalize">Access</div>
                    <div class="text-capitalize">Management</div>
                </div>

                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                    aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>

                <div class="collapse navbar-collapse" id="navbarSupportedContent">

                    <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
                        <button type="button" class="btn btn-outline-secondary btn-sm rounded-pill"
                            style="font-size: 16px; padding: 8px 5px; width: 100px; border-radius: 5px;">
                            <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="currentColor"
                                class="bi bi-person-circle" viewBox="0 0 16 16">
                                <path d="M11 6a3 3 0 1 1-6 0 3 3 0 0 1 6 0" />
                                <path fill-rule="evenodd"
                                    d="M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8m8-7a7 7 0 0 0-5.468 11.37C3.242 11.226 4.805 10 8 10s4.757 1.225 5.468 2.37A7 7 0 0 0 8 1" />
                            </svg>
                            <nuxt-link to="/login">
                                <li class="nav-item loginBtn" style="float: right; text-align: center; line-height: 32px;">
                                    Login
                                </li>
                            </nuxt-link>
                        </button>
                    </ul>
                </div>
            </div>
        </nav>
    </div>
</template>

<script>

</script>

<style></style>