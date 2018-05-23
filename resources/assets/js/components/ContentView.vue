<template>
  <!-- Display the page -->
  <div class="column is-8">
    <section class="hero is-primary">
      <div class="hero-body" :style="{ backgroundImage: 'url(' + heroUrl + ')' }">
        <div class="container">
          <h1 class="title">
            {{ heading }}
          </h1>
          <h2 class="subtitle">
            {{ subtitle }}
          </h2>
        </div>
      </div>
    </section>

    <section class="hero is-light is-bold">
      <div class="hero-body">
        <div class="text-center" v-html="content">
        </div>
        <div class="columns">
          <div v-for="(row, index) in rows" class="column">

            <div class="card">

              <div class="card-image">
                  <img v-if="row.url" :src="row.url" :alt="row.title">
                  <img v-else src="https://bulma.io/images/placeholders/1280x960.png" alt="Placeholder image">
              </div>

              <div class="card-content">

                <div class="title is-4">{{ row.title }}</div>

                <div class="content">
                  {{ row.description }}
                </div>

              </div>
            </div>

          </div>
        </div>

      </div>
    </section>
</div>

</template>
