<svelte:head>
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: "Roboto";
        }
    </style>
</svelte:head>
<script>
    import axios from 'axios';
    import { DateTime } from 'luxon';
    import Post from './Post.svelte';
    let startDate = DateTime.now().minus({ months: 2 }).toISODate();
    let endDate = DateTime.now().minus({ months: 1 }).toISODate();
    let after, promise, lastPostId;

    $: {
        // this function will close over the new after, startDate and endDate
        async function getRedditPosts() {
            let { data: { data: { children: res } } } = await axios.get(`https://www.reddit.com/r/TikTokCringe/top.json?t=year&limit=100${after !== undefined ? `&after=t3_${after}` : ''}`);
            const start = DateTime.fromISO(startDate).toSeconds();
            const end = DateTime.fromISO(endDate).toSeconds();
            res = res.filter(post => {
                const { created } = post.data;
                return created > start && created < end;
            })
            res = res.filter(post => {
                const { link_flair_text } = post.data;
                return !["Politics"].includes(link_flair_text);
            })
            lastPostId = res[res.length - 1]?.data.id ?? undefined;
            return res;
        }
        
        promise = getRedditPosts();
    }

    const handleClick = () => {
        after = lastPostId;
    }

    const handleDateChange = () => {
        after = undefined;
    }

</script>

<main class="max-w-3xl mx-auto space-y-2 py-4">
    <div class="flex justify-center p-4 space-x-2">
        <div>
            <label for="startDate">Start date</label>
            <input type='date' id="startDate" name="startDate" on:change={handleDateChange} bind:value={startDate}/>
        </div>
        <div>
            <label for="endDate">End date</label>
            <input type='date' id="endDate" name="endDate" on:change={handleDateChange} bind:value={endDate}/>
        </div>
    </div>
    <div class="flex flex-col space-y-2">
        {#await promise}
            <!-- promise is pending -->
            <div class="flex relative justify-center items-center h-[175px]">
                <div class="ring-of-dots"/>
            </div>
        {:then posts}
            <!-- promise was fulfilled -->
            {#if posts.length === 0}
                No more posts.
            {:else}
                {#each posts as {
                        data: {
                            title,
                            thumbnail,
                            permalink,
                            score,
                            created,
                            id,
                            link_flair_text,
                            media,
                            preview
                        }
                    }
                }
                    <Post 
                         previewUrl={preview?.images[0]?.resolutions[2]?.url}
                         videoUrl={media?.reddit_video?.fallback_url}
                         permalink={permalink}
                         flair={link_flair_text}
                         id={id}
                         title={title}
                         score={score}
                         created={created}
                        />
                {/each}
            {/if}
        {:catch error}
            <!-- promise was rejected -->
            <p>Something went wrong: {error.message}</p>
        {/await}
        <button class="p-4" type="button" on:click={() => handleClick()}>NEXT</button>
    </div>
</main>

<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  body {
      @apply bg-gray-500 text-white;
  }

  input[type="date"] {
      @apply text-black;
  }

  :root {
      --loading-half-color: #919191;
      --loading-full-color: #5e5e5e;
  }

  /**
  * Ring of dots
  *
  * @author jh3y
*/
  @-webkit-keyframes ring-of-dots {
  0% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); }
  14.28571% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white; }
  28.57143% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  42.85714% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  57.14286% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  71.42857% {
    -webkit-box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  85.71429% {
    -webkit-box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color);
            box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color); }
  100% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); } }
@keyframes ring-of-dots {
  0% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); }
  14.28571% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 var(--loading-half-color), -4.45042px -19.49856px 0 0 var(--loading-full-color), 12.4698px -15.63663px 0 0 white; }
  28.57143% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 var(--loading-half-color), -18.01938px -8.67767px 0 0 var(--loading-full-color), -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  42.85714% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 var(--loading-half-color), -18.01938px 8.67767px 0 0 var(--loading-full-color), -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  57.14286% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 var(--loading-half-color), -4.45042px 19.49856px 0 0 var(--loading-full-color), -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  71.42857% {
    -webkit-box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white;
            box-shadow: 20px 0px 0 0 var(--loading-half-color), 12.4698px 15.63663px 0 0 var(--loading-full-color), -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 white; }
  85.71429% {
    -webkit-box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color);
            box-shadow: 20px 0px 0 0 var(--loading-full-color), 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 white, 12.4698px -15.63663px 0 0 var(--loading-half-color); }
  100% {
    -webkit-box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color);
            box-shadow: 20px 0px 0 0 white, 12.4698px 15.63663px 0 0 white, -4.45042px 19.49856px 0 0 white, -18.01938px 8.67767px 0 0 white, -18.01938px -8.67767px 0 0 white, -4.45042px -19.49856px 0 0 var(--loading-half-color), 12.4698px -15.63663px 0 0 var(--loading-full-color); } }


.ring-of-dots:before {
  animation: ring-of-dots 1s infinite linear reverse;
  border-radius: 10px;
  content: '';
  display: block;
  height: 10px;
  width: 10px; }
</style>
