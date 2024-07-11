<template>
  <!-- Posts -->
  <ul>
    <li v-for="post in posts" :key="post.id" class="flex gap-3">
      <img
        v-if="post.user.avatar_url"
        class="w-14 h-14 rounded-full ml-3"
        :src="post.user.avatar_url"
        alt="User Avatar"
      />
      <div class="flex border-2 border-red-500">
        <div>
          <div class="flex gap-3 mb-2">
            <p>{{ post.user.name }}</p>
            <p>@{{ post.user.user_name }}</p>
            <p>. 5h</p>
          </div>
          <p class="w-[80%] mb-4">
            {{ post.content }}
          </p>
          <img
            v-if="post.image_url"
            :src="post.image_url"
            alt="Post Image"
            class="w-[80%] h-auto rounded-3xl border border-[lightgray]"
          />
          <div class="post-icns flex justify-between w-[80%] p-5">
            <p>
              <img src="../assets/icons/comments.svg" alt="" />{{
                formatNumber(post.likes_count)
              }}
            </p>
            <p>
              <img src="../assets/icons/comments.svg" alt="" />{{
                formatNumber(post.likes_count)
              }}
            </p>
            <p>
              <img src="../assets/icons/comments.svg" alt="" />{{
                formatNumber(post.likes_count)
              }}
            </p>
            <p>
              <img src="../assets/icons/comments.svg" alt="" />{{
                formatNumber(post.likes_count)
              }}
            </p>
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
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  name: "PostsContainer",
  setup() {
    const posts = ref([]);

    async function fetchPosts() {
      try {
        const postsResponse = await axios.get("http://localhost:3000/Posts");
        const usersResponse = await axios.get("http://localhost:3000/Users");

        const usersMap = usersResponse.data.reduce((acc, user) => {
          acc[user.id] = user;
          return acc;
        }, {});

        posts.value = postsResponse.data.map((post) => ({
          ...post,
          user: usersMap[post.user_id],
        }));
      } catch (error) {
        console.error("Error fetching posts:", error);
      }
    }

    function formatNumber(number) {
      if (number >= 1000000000) {
        return (number / 1000000000).toFixed(1) + "B";
      } else if (number >= 1000000) {
        return (number / 1000000).toFixed(1) + "M";
      } else if (number >= 1000) {
        return (number / 1000).toFixed(1) + "K";
      }
      return number;
    }

    onMounted(fetchPosts);

    return {
      posts,
      formatNumber,
    };
  },
};
</script>
