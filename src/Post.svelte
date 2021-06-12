<script>
    import { DateTime } from 'luxon';
    export let videoUrl, previewUrl, permalink, flair, id, title, score, created;
    const tagBackgroundColors = {
        'Cringe': '#ea0027',
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
</script>

<div class="grid grid-cols-3 grid-gap-2 rounded-md bg-gray-300">
    <div class="col-span-1 md:col-span-2">
        <video height="488px" class="max-h-[488px] !w-full" controls poster={previewUrl.replaceAll('amp;', '')}>
            <source src={videoUrl} type="video/mp4">
        </video>
    </div>
    <div class="flex flex-col space-y-2 p-2 col-span-2 md:col-span-1">
        <span class="rounded-full p-2 w-[fit-content] text-white font-medium cursor-default" style={`background-color: ${tagBackgroundColors[flair]}`}>{flair}</span>
        <a href={`https://reddit.com${permalink}`} target="_blank">
            <!--
                <img src={thumbnail} onerror="if (this.src != 'error.jpg') this.src = '/images/not-found.svg';" class='!h-[488px] !w-[488px]'/>
            -->
            <div class="details">
                <span><span class="font-bold">{id}</span>: {@html title}</span>
                <span class="font-medium text-blue-500">{score}</span>
                <time datetime={DateTime.fromSeconds(created).toISODate()}>{DateTime.fromSeconds(created).toISODate()}</time>
            </div>
        </a>
    </div>
</div>

<style>
    .details {
        @apply flex flex-col space-y-2 text-black;
    }
    a {
        @apply hover:no-underline;
    }
</style>

