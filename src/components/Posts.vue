<template>
  <!-- Posts -->
  <ul class="posts">
    <li v-for="post in filteredPosts()" :key="post.id" class="flex gap-3">
      <img
        v-if="post.user.avatar_url"
        class="w-14 h-14 rounded-full ml-3"
        :src="require(`@/${post.user.avatar_url}`)"
        alt="User Avatar"
      />

      <div class="w-full h-full">
        <div class="flex gap-3 mb-2">
          <p>{{ post.user ? post.user.name : "Unknown User" }}</p>
          <p>@{{ post.user ? post.user.user_name : "unknown" }}</p>
          <p>. 5h</p>
        </div>

        <p class="w-[70%] mb-4">
          {{ post.content }}
        </p>
        <img
          v-if="post.image_url"
          :src="require(`@/${post.image_url}`)"
          alt="Post Image"
          class="w-[70%] rounded-3xl border border-[lightgray]"
        />
        <div class="w-[40%] post-icns flex justify-between p-5">
          <p @click="toggleLike(post)">
            <img
              :src="
                post.liked
                  ? require('../assets/icons/heartLiked.svg')
                  : require('../assets/icons/heart.svg')
              "
              alt="Heart Icon"
            />
            {{ formatNumber(post.likes_count) }}
          </p>
          <p @click="toggleCommentForm(post.id)">
            <img src="../assets/icons/comments.svg" alt="" />
            {{ formatNumber(post.comments_count) }}
          </p>
        </div>
        <CommentForm
          v-if="activePost === post.id"
          :postId="post.id"
          :userId="1"
          @commentSubmitted="updateCommentCount(post.id)"
        />
      </div>
    </li>
  </ul>
</template>

<style>
body {
  color: white;
}

.post-icns p {
  display: flex;
  gap: 8px;
  cursor: pointer;
}

.posts li {
  padding-top: 12px;
  border-bottom: 1px solid lightgray;
}
</style>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";
import CommentForm from "./CommentForm.vue";

export default {
  name: "PostsContainer",
  components: {
    CommentForm,
  },
  props: {
    searchQuery: {
      type: String,
      default: "",
    },
  },
  setup(props) {
    const posts = ref([]);
    const activePost = ref(null);

    async function fetchPosts() {
      try {
        const [postsResponse, usersResponse] = await Promise.all([
          axios.get("http://localhost:3000/Posts"),
          axios.get("http://localhost:3000/Users"),
        ]);

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

    async function toggleLike(post) {
      try {
        const updatedPost = {
          ...post,
          liked: !post.liked,
          likes_count: post.liked ? post.likes_count - 1 : post.likes_count + 1,
        };

        await axios.put(`http://localhost:3000/Posts/${post.id}`, updatedPost);

        const index = posts.value.findIndex((p) => p.id === post.id);
        if (index !== -1) {
          posts.value[index] = { ...updatedPost, user: post.user };
        }
      } catch (error) {
        console.error("Error toggling like:", error);
      }
    }

    async function updateCommentCount(postId) {
      if (activePost.value === postId) {
        activePost.value = null;
      } else {
        activePost.value = postId;
      }

      try {
        const index = posts.value.findIndex((post) => post.id === postId);
        if (index !== -1) {
          const updatedPost = {
            ...posts.value[index],
            comments_count: posts.value[index].comments_count + 1,
          };

          await axios.put(`http://localhost:3000/Posts/${postId}`, updatedPost);
          posts.value[index] = updatedPost;
        }
      } catch (error) {
        console.error(
          `Error updating comment count for post ${postId}:`,
          error
        );
      }
    }

    function toggleCommentForm(postId) {
      if (activePost.value === postId) {
        activePost.value = null;
      } else {
        activePost.value = postId;
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

    function filteredPosts() {
      if (!props.searchQuery) {
        return posts.value;
      }
      return posts.value.filter((post) =>
        post.user.user_name
          .toLowerCase()
          .includes(props.searchQuery.toLowerCase())
      );
    }

    onMounted(fetchPosts);

    return {
      posts,
      formatNumber,
      toggleLike,
      filteredPosts,
      activePost,
      toggleCommentForm,
      updateCommentCount,
    };
  },
};
</script>
