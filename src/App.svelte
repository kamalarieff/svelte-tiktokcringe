<script>
    import axios from 'axios';
    import { DateTime } from 'luxon';
	export let name;
    let startDate = DateTime.now().minus({ months: 2 }).toISODate();
    let endDate = DateTime.now().minus({ months: 1 }).toISODate();
    let after;
    let promise;
    let lastPostId;
    
    const tagBackgroundColors = {
        'Humor/Cringe': '#7c5295',
        'Humor': '#24a0ed',
        'Cool': '#ddbd37',
        'Wholesome': 'rgb(148, 224, 68)',
        'Wholesome/Humor': 'rgb(0, 139, 139)',
        'Duet Troll': 'rgb(255, 135, 23)',
        'OC (I made this)': 'rgb(255, 102, 172)',
        'Cursed': 'rgb(26, 26, 27)',
        'Politics': 'rgb(160, 99, 36)',
        'Discussion': 'rgb(13, 211, 187)'
    };

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

</script>

<main class="max-w-3xl mx-auto space-y-2 py-4">
    <div class="flex justify-center p-4 space-x-2">
        <div>
            <label for="startDate">Start date</label>
            <input type='date' id="startDate" name="startDate" bind:value={startDate}/>
        </div>
        <div>
            <label for="endDate">End date</label>
            <input type='date' id="endDate" name="endDate" bind:value={endDate}/>
        </div>
    </div>
    <div class="flex flex-col space-y-2">
        {#await promise}
            <!-- promise is pending -->
            <p>Loading...</p>
        {:then posts}
            <!-- promise was fulfilled -->
            {#if posts.length === 0}
                No more posts.
            {:else}
                {#each posts as {
                        data: {
                            title,
                            thumbnail,
                            thumbnail_width,
                            thumbnail_height,
                            permalink,
                            full_link,
                            score,
                            url,
                            created,
                            id,
                            link_flair_text,
                            media,
                            preview
                        }
                    }
                }
                    <div class="grid grid-cols-3 grid-gap-2 rounded-md bg-gray-300">
                        <div class="col-span-1 md:col-span-2">
                            <video height="488px" class="max-h-[488px] !w-full" controls poster={preview?.images[0]?.resolutions[2]?.url.replaceAll('amp;', '')}>
                                <source src={media?.reddit_video?.fallback_url} type="video/mp4">
                            </video>
                        </div>
                        <div class="flex flex-col space-y-2 border border-gray-200 p-2 col-span-2 md:col-span-1">
                            <span class="rounded-full p-2 w-[fit-content] text-white font-medium" style={`background-color: ${tagBackgroundColors[link_flair_text]}`}>{link_flair_text}</span>
                            <a href={`https://reddit.com${permalink}`} target="_blank">
                                <!--
                                    <img src={thumbnail} onerror="if (this.src != 'error.jpg') this.src = '/images/not-found.svg';" class='!h-[488px] !w-[488px]'/>
                                -->
                                <div class="flex flex-col space-y-2">
                                    <span><span class="font-bold">{id}</span>: {title}</span>
                                    <span class="font-medium text-blue-500">{score}</span>
                                    <time datetime={DateTime.fromSeconds(created).toISODate()}>{DateTime.fromSeconds(created).toISODate()}</time>
                                </div>
                            </a>
                        </div>
                    </div>
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
</style>
