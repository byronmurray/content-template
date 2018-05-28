<template>
  <!-- Navbar block -->
  <nav v-if="logoUrl" class="navbar is-transparent">
    <div class="navbar-brand">
      <a class="navbar-item" href="#">
        <img :src="logoUrl" :alt="name" >
      </a>
      <div class="navbar-burger burger" data-target="navbarExampleTransparentExample">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>

    <div id="navbarExampleTransparentExample" class="navbar-menu">

      <div class="navbar-end">
        <a class="navbar-item" href="#">
          Home
        </a>
      </div>

    </div>

  </nav>
</template>
