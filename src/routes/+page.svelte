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
        <button on:click={() => reset()}>초기화</button>
    </div>

    <div>
        <svg height="400" width="400">
            <g transform="translate(200,200)">
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
                    <g transform={`rotate(${angle})`} on:click={() => click()} on:transitionend={transitionend}>
                        {#each options as opt, i}
                            <Arc r={r} a0={(360 / options.length)*i} a1={(360 / options.length)*(i+1)} />
                        {/each}
                        {#each options as opt, i}
                        <ArcLabel r={r*2.0/3.0} a={(360 / options.length)*(i+0.5)} text={opt} />
                        {/each}
                    </g>
                {/if}
            {/if}
            <!-- 5개 최대 12자 -->
            <!-- 7개 최대 8자 -->
            <!-- 그 이상 4자 -->
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
    let input_value = "";
    let r = 150;
    let angle = (360 / options.length) / 2;

    function onClickTopic() {
        options = [...options, input_value];
        angle = (360 / options.length) / 2
        asd++;
        setTimeout(function() {
            asd++;
        }, 1);
        input_value = ""
    }
    function randint(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min
    }

    function randfloat(min, max) {
      return Math.random() * (max - min) + min
    }

    function roundUp(x, z) {
      return Math.ceil(x / z) * z
    }
    let rolledOption = 0;
    function click() {
        console.log("click", angle);
        let roll = randint(0, options.length-1)
        let rollPlace = randfloat(0.2*(360 / options.length), 0.8*(360 / options.length))
        let finalAngle = roll * (360 / options.length) + rollPlace
        let spins = randint(2, 3)
        angle = roundUp(angle, 360) + spins * 360 + finalAngle
        console.log("new", angle);
        rolledOption = options[roll]
    }
    function transitionend() {
        console.log("transitionend");
    }
    function reset() {
        options = []
        input_value = ""
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
g {
    transition: 3s ease-out;
  }
</style>

