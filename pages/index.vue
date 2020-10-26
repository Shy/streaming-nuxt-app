<template>
  <div class="container my-12 mx-auto px-4 md:px-12">
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
      <div
        v-for="run in data.runsCollection.items"
        class="my-1 px-1 w-full md:w-1/2 lg:my-4 lg:px-4 lg:w-1/3"
      >
        <article class="overflow-hidden rounded-lg shadow-lg">
          <a href="#">
            <img
              alt="Placeholder"
              class="block h-auto w-full"
              :src="run.heartRate.url"
              :alt="run.heartRate.title"
            />
          </a>

          <header
            class="flex items-center justify-between leading-tight p-2 md:p-4"
          >
            <h1 class="text-lg">
              <a class="no-underline hover:underline text-black" href="#">
                {{ run.routeName }}
              </a>
            </h1>
            <p class="text-grey-darker text-sm">
              {{ new Date(run.date).toISOString().split("T")[0] }}
            </p>
          </header>

          <footer
            class="flex items-center justify-between leading-none p-2 md:p-4"
          >
            <a
              class="flex items-center no-underline hover:underline text-black"
              href="#"
            >
              <img
                class="block rounded-full"
                :src="run.runner.photo.url"
                :alt="run.runner.photo.title"
              />
              <p class="ml-2 text-sm">{{ run.runner.name }}</p>
            </a>
            <a
              class="no-underline text-grey-darker hovsr:text-red-dark"
              href="#"
            >
              <span class="hidden">Like</span>
              <i class="fa fa-heart"></i>
            </a>
          </footer>
        </article>
        <!-- END Article -->
      </div>
      <!-- END Column -->
    </div>
  </div>
</template>

<script>
import { gql } from "graphql-request";
export default {
  async asyncData({ $graphql, params }) {
    const query = gql`
      query {
        runsCollection {
          items {
            routeName
            date
            heartRate {
              title
              url
            }
            distanceInMiles
            runner {
              name
              photo {
                title
                url(transform: { width: 32, height: 32 })
              }
            }
          }
        }
      }
    `;
    const data = await $graphql.request(query);
    console.log(data.runsCollection);
    return { data };
  },
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
gh .title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
