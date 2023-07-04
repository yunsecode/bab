<!-- svelte-ignore a11y-click-events-have-key-events -->
<div id="bab">
    <h1 class="phrase">
        <div class="phrase-text quote">
            "인생은 낮저밤이"
        </div>
        <div class="phrase-text">
            낮에는 저거 먹고 밤에는 이거 먹고
        </div>
    </h1>
    <div class="food-input">
        <input bind:value={input_value}>
        <button on:click={() => onClickTopic()}>추가</button>
    </div>

    <div>
        asd {asd} <br/>
        oprions {options} <br/>
        aaa{options.length}
        <svg height="400" width="400">
            bbb{options.length}
            <g transform="translate(200,200)">
              ccc{options.length}
            <!-- =========================================== -->
            {#if asd %2 == 0}
                {#if options.length == 0}
                    <g transform={`rotate(${0})`} on:click={() => click()} on:transitionend={transitionend}>
                        <FullArc r={r} />
                    </g>
                {:else if options.length == 1}
                    <g transform={`rotate(${0})`} on:click={() => click()} on:transitionend={transitionend}>
                        <FullArc r={r} />
                        {#each options as opt, i}
                            <ArcLabel r={r*2.0/3.0} a={360*(i+0.5)} text={opt} />
                        {/each}
                    </g>
                {:else}
                    <g transform={`rotate(${(360 / options.length) / 2})`} on:click={() => click()} on:transitionend={transitionend}>
                        {#each options as opt, i}
                            <Arc r={r} a0={(360 / options.length)*i} a1={(360 / options.length)*(i+1)} />
                        {/each}
                    </g>
                {/if}
            {/if}
            <!-- =========================================== -->
          </g>
          <polygon points="200 360 210 370 190 370"/>
        </svg>
      </div>
</div>

<script>
    import RouletteWheel from "../components/RouletteWheel.svelte"
    import FullArc from "../components/FullArc.svelte";
    import ArcLabel from "../components/ArcLabel.svelte";
    import Arc from "../components/Arc.svelte";
    let options = [];
    let asd = 0;
    let input_value = 0;
    let r = 150;

    function onRolled(opt) {
        console.log(opt)
    }
    function onClickTopic() {
        options = [...options, input_value];
        asd++;
        console.log(111);
        setTimeout(function() {
            asd++;
        // 원하는 작업을 수행하는 코드
        }, 1);
    }
    function click() {

    }
    function transitionend() {
        console.log("transitionend");
    //   onRolled(rolledOption)
    }
</script>

<style lang="scss" scoped>
#bab {
    .phrase {
        @media (max-width: 640px){
            font-size: medium;
        }
        .phrase-text {
            display: flex;
            justify-content: center;
        }
        .quote {
        }

    }
    .food-input {
        display: flex;
        justify-content: center;
        gap: 20px;
    }
}
:global(body) {
  background-color: #444;
  color: #fff;
  margin: 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  user-select: none;
}

svg {
  display: block;
}

polygon {
  fill: yellow;
}
</style>

