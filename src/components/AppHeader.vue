<template>
    <nav class="navbar navbar-dark bg-dark">
        <a href="/" class="navbar-brand">ỨNG DỤNG QUẢN LÍ DANH BẠ</a>
        <div class="mr-auto navbar-nav">
            <li class="nav-item">
                <router-link :to="{ name: 'contactbook' }" class="navlink text-right">
                    Danh bạ
                    <i class="fas fa-address-book"></i>
                </router-link>
            </li>
        </div>
    </nav>
</template>