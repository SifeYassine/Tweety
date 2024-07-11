<template>
  <!-- Tweet Bar -->
  <nav class="p-4 border-[1px] border-[lightgray]">
    <div>
      <div class="flex">
        <img
          class="w-10 h-10 rounded-full"
          src="../assets/Profile.png"
          alt=""
        />
        <div class="w-[70%]">
          <input
            type="text"
            placeholder="What's happening?"
            class="w-full h-10 ml-5 pl-4 border-[1px] border-[lightgray] rounded-full"
          />

          <div class="flex ml-6">
            <label for="twtImg" class="cursor-pointer">
              <img src="../assets/icons/imgTweet.svg" alt="" />
            </label>
            <input type="file" id="twtImg" class="hidden" />
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style>
nav {
  height: fit-content;
}
</style>

<script>
export default {
  name: "TweetBar",
};
</script>
