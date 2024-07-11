<template>
  <!-- Posts -->
  <ul>
    <li class="flex gap-3">
      <img
        class="w-14 h-14 rounded-full ml-3"
        src="../assets/Profile.png"
        alt=""
      />
      <div class="flex border-2 border-red-500">
        <div>
          <div class="flex gap-3 mb-2">
            <p>Full Name</p>
            <p>@username</p>
            <p>. 5h</p>
          </div>
          <p class="w-[80%] mb-4">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Iusto aut
            quaerat officia voluptatem ut exercitationem sint dignissimos
            impedit expedita in cumque.
          </p>
          <img
            src="../assets/Profile.png"
            alt="Post Image"
            class="w-[80%] h-auto rounded-3xl border border-[lightgray]"
          />

          <div class="post-icns flex justify-between w-[80%] p-5">
            <p><img src="../assets/icons/comments.svg" alt="" />3</p>
            <p><img src="../assets/icons/comments.svg" alt="" />3</p>
            <p><img src="../assets/icons/comments.svg" alt="" />3</p>
            <p><img src="../assets/icons/comments.svg" alt="" />3</p>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<style>
body {
  color: antiquewhite;
}

li {
  height: fit-content;
}

.post-icns p {
  display: flex;
  gap: 8px;
  cursor: pointer;
}
</style>

<script>
export default {
  name: "PostsContainer",
};
</script>
