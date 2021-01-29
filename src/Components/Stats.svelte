<script>
	import ChessLine from './ChessLine.svelte'

    export let obj;
    $: ({chess_daily, chess_rapid, chess_bullet, chess_blitz} = obj);

    const hasDaily = chess_daily === undefined;
    const hasRapid = chess_rapid === undefined;
    const hasBullet = chess_bullet === undefined;
    const hasBlitz = chess_blitz === undefined;

    const rating = (obj, playType) => {
        let hasCategory = obj.hasOwnProperty(playType);
        let hasRtg = false;
        if (hasCategory) {
            hasRtg = obj[playType].hasOwnProperty('rating');
        }

        if (!hasCategory || !hasRtg){
            return "N/A"
        }
        else {
            return obj[playType].rating;
        }
    }

</script>

{#if hasDaily}
<ChessLine 
    gameType={"Daily Chess"}
    currRtg={rating(chess_daily, 'last')}
    bestRtg={rating(chess_daily, 'best') === "N/A" ? rating(chess_daily, 'last') : rating(chess_daily, 'best')} 
/>
{/if}

{#if hasRapid}
<ChessLine 
    gameType={"Rapid Chess"}
    currRtg={rating(chess_rapid, 'last')}
    bestRtg={rating(chess_rapid, 'best') === "N/A" ? rating(chess_rapid, 'last') : rating(chess_rapid, 'best')} 
/>
{/if}

{#if hasBullet}
<ChessLine 
    gameType={"Bullet Chess"}
    currRtg={rating(chess_bullet, 'last')}
    bestRtg={rating(chess_bullet, 'best') === "N/A" ? rating(chess_bullet, 'last') : rating(chess_bullet, 'best')} 
/>
{/if}

{#if hasBlitz}
<ChessLine 
    gameType={"Blitz Chess"}
    currRtg={rating(chess_blitz, 'last')}
    bestRtg={rating(chess_blitz, 'best') === "N/A" ? rating(chess_blitz, 'last') : rating(chess_blitz, 'best')} 
/>
{/if}

