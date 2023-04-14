<template>
  <div class="max-w-screen-md mt-6 mx-auto w-72">
    <Content class="text-center"></Content>
    <div class="mt-10">
      <small class="text-left">
        Assalamu'alaikum.<br>
        Feel free to use this simple surah picker for your hifdh revision, tadabbur, recitation in your solah, or however you like.<br>
        For more specific result, "Pick a surah from" the list of Quran division.<br>
        Why Quran division is preferred over Juz list?<br>
        I would like to invite you to read <a href="https://tulayhah.wordpress.com/2018/05/07/how-the-sahabah-read-and-divided-the-quran-ibn-taymiyah/" class="underline" target="_blank">this article</a>.<br>
        Wa billahi tawfiq.
      </small>
    </div>
    <footer class="flex items-center justify-between text-center my-8 mx-auto">
      <h1 class="font-extrabold uppercase">Suwar Shuffler</h1>
      <p>{{ (new Date).getFullYear() }} <a href="https://bio.link/bintazud" target="_blank" class="underline">BintAzud</a></p>
    </footer>
  </div>
</template>

<script>
import Content from './components/Content.vue'

export default {
  name: 'App',
  components: {
    Content
  },
  created(){
    document.title = "Suwar Shuffler"
  }
}
</script>
