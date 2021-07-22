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
    import { of } from 'rxjs';
    import { toArray, mergeMap, last, concatMap, share, filter } from 'rxjs/operators';
    import axios from 'axios';
    import { DateTime } from 'luxon';
    import Post from './Post.svelte';
    import Spinner from './Spinner.svelte';

    let startDate = DateTime.now().minus({ months: 2 }).toISODate();
    let endDate = DateTime.now().toISODate();
    let lastPostId;
    let arrOfRes = [];
    let page = 0;
    const MAX_PAGES = 5;

    const handleClick = () => {
        page++;
        window.scrollTo(0, 0);
    }

    const handleDateChange = () => {
        arrOfRes = [];
        page = 0;
        lastPostId = undefined;
    }
 
    // This is still the best way to stop fetching more posts
    $: if (arrOfRes.length - page < MAX_PAGES) {
        let observable$ = of(lastPostId).pipe(
            concatMap(lastPostId => {
                // With the new way of setting the lastPostId, this will always return the same result
                // A good idea would be to store this and only filter from it
                return axios.get(`https://www.reddit.com/r/TikTokCringe/top.json?t=year&limit=100${lastPostId !== undefined ? `&after=t3_${lastPostId}` : ''}`);
            }),
            // convert the array to individual events
            mergeMap(res => {
                return res.data.data.children;
            }),
            // this will enable future observable to be only operated once
            share()
        );

        // Gets the last id in the observable
        observable$.pipe(
            last()
        ).subscribe(res => {
            lastPostId = res.data.id;
        });

        // Filter out the posts
        observable$.pipe(
            filter(post => {
                const { created } = post.data;
                const start = DateTime.fromISO(startDate).toSeconds();
                const end = DateTime.fromISO(endDate).toSeconds();
                return created > start && created < end;
            }),
            filter(post => {
                const { link_flair_text } = post.data;
                return !["Politics"].includes(link_flair_text);
            }),
            toArray()
        ).subscribe(res => {
            arrOfRes = arrOfRes.concat([ res ]);
        });
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
        {#if arrOfRes.length === 0}
            <div class="h-[175px] flex justify-center items-center">
                No more posts.
            </div>
        {:else}
            {#each arrOfRes[page] as {
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
                     previewUrl={preview?.images[0]?.resolutions[2]?.url ?? ""}
                     videoUrl={media?.reddit_video?.fallback_url ?? ""}
                     permalink={permalink}
                     flair={link_flair_text}
                     id={id}
                     title={title}
                     score={score}
                     created={created}
                    />
            {/each}
        {/if}
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
