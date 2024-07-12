<template>
  <div class="comment-form flex flex-col gap-3 w-[50%]">
    <input
      type="text"
      v-model="comment"
      placeholder="Write a comment..."
      @keyup.enter="submitComment"
      class="w-full h-10 pl-4 border-[1px] border-[lightgray] rounded-full"
    />
    <button
      @click="submitComment"
      class="w-[50%] rounded-full cursor-pointer p-2 bg-blue-500"
    >
      Submit
    </button>
  </div>

  <ul class="mt-5">
    <li
      v-for="comment in comments"
      :key="comment.id"
      class="w-[50%] border-[1px] border-[lightgray] rounded-xl my-1 p-3"
    >
      <p class="text-gray-300 font-bold">{{ comment.user.user_name }}</p>
      <p>{{ comment.comment }}</p>
    </li>
  </ul>
</template>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  props: {
    postId: {
      type: Number,
      required: true,
    },
  },
  emits: ["commentSubmitted"],
  setup(props, { emit }) {
    const comment = ref("");
    const comments = ref([]);

    async function fetchComments() {
      try {
        const response = await axios.get("http://localhost:3000/Comments");
        comments.value = response.data.filter(
          (comment) => comment.post_id === props.postId
        );
      } catch (error) {
        console.error("Error fetching comments:", error);
      }
    }

    async function submitComment() {
      if (!comment.value.trim()) return;

      try {
        const response = await axios.get("http://localhost:3000/Comments");
        const lastId =
          response.data.length > 0
            ? parseInt(response.data[response.data.length - 1].id)
            : 0;
        const newId = lastId + 1;

        const newComment = {
          id: newId.toString(),
          comment: comment.value,
          created_at: new Date().toISOString(),
          user_id: "1",
          post_id: props.postId,
          user: {
            id: "1",
            user_name: "Sife1",
          },
        };

        await axios.post("http://localhost:3000/Comments", newComment);

        comments.value.push(newComment);
        comment.value = "";

        emit("commentSubmitted", props.postId);
      } catch (error) {
        console.error("Error adding comment:", error);
        alert("Comment submission failed");
      }
    }

    onMounted(fetchComments);

    return {
      comment,
      comments,
      submitComment,
    };
  },
};
</script>
