<svelte:head>
    <title>TikTokCringe's Top Posts</title>
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: "Roboto";
        }
    </style>
    <link rel="shortcut icon" href="https://styles.redditmedia.com/t5_mvcq5/styles/communityIcon_40dp09kc5vw41.png?width=256&s=67858eae97c8b471bec4e1e51d4cf4f5df940f42" />
</svelte:head>
<script>
    import axios from 'axios';
    import { DateTime } from 'luxon';
    import Post from './Post.svelte';
    import Spinner from './Spinner.svelte';
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
            <Spinner />
        {:then posts}
            <!-- promise was fulfilled -->
            {#if posts.length === 0}
                <div class="h-[175px] flex justify-center items-center">
                    No more posts.
                </div>
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
        <button class="p-4 bg-white text-black" type="button" on:click={() => handleClick()}>NEXT</button>
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

</style>
