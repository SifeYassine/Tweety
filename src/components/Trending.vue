<template>
  <!-- Trending Bar -->
  <aside class="w-[25vw] h-auto border-[1px] border-[lightgray] rounded-[20px]">
    <ul class="trending">
      <li>
        <h1 class="text-xl font-bold">Trending for you</h1>
      </li>
      <li>
        <p>Trending in Worldwide</p>
        <h3>USA Elections</h3>
        <p>11.4k Tweets</p>
      </li>

      <li>
        <p>Trending in Worldwide</p>
        <h3>Coronavirus</h3>
        <p>8.2M Tweets</p>
      </li>

      <li>
        <p>Trending in Morocco</p>
        <h3>Drought in Morocco</h3>
        <p>1.2k Tweets</p>
      </li>

      <li>
        <p>Trending in USA</p>
        <h3>Coronavirus</h3>
        <p>8.2M Tweets</p>
      </li>

      <li>
        <p>Trending in Morocco</p>
        <h3>Drought in Morocco</h3>
        <p>1.2k Tweets</p>
      </li>

      <li>
        <p>Trending in USA</p>
        <h3>Coronavirus</h3>
        <p>8.2M Tweets</p>
      </li>
    </ul>
  </aside>
</template>

<style>
.trending li {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  color: antiquewhite;
  padding: 12px 30px;
  border-bottom: 1px solid lightgray;
}

.trending li:last-child {
  border-bottom: none;
}

.trending li p {
  color: gray;
  font-size: 13px;
}
</style>

<script>
export default {
  name: "TrendingBar",
};
</script>
