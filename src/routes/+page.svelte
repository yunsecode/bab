<!-- svelte-ignore a11y-click-events-have-key-events -->
<div id="bab">
    <!-- phrase -->
    <h1 class="phrase">
        <div class="phrase-text quote">
            "인생은 낮저밤이"
        </div>
        <div class="phrase-text">
            낮에는 저거 먹고 밤에는 이거 먹고
        </div>
    </h1>

    <!-- input -->
    <div class="food-input">
        <input bind:value={input_value}>
        <button on:click={() => clickAddElement()}>추가</button>
        <button on:click={() => clickResetElement()}>초기화</button>
    </div>

    <!-- roulette -->
    <div>
        <svg height="400" width="400">
            <!-- roulette in center -->
            <g transform="translate(200,200)">
                <!-- circle -->
                {#if tick % 2 == 0}
                    {#if elements.length == 0}
                        <g transform={`rotate(${0})`}>
                            <FullArc r={r} />
                        </g>
                    {:else if elements.length == 1}
                        <g transform={`rotate(${0})`}>
                            <FullArc r={r} />
                            {#each elements as opt, i}
                                <ArcLabel r={r*2.0/3.0} a={360*(i+0.5)} text={opt} />
                            {/each}
                        </g>
                    {:else}
                        <g id="hello" style="transform: rotate({angle}deg);" on:click={() => click()} on:transitionend={transitionend}>
                            {#each elements as opt, i}
                                <Arc r={r} a0={(360 / elements.length)*i} a1={(360 / elements.length)*(i+1)} />
                            {/each}
                            {#each elements as opt, i}
                                <ArcLabel r={r*2.0/3.0} a={(360 / elements.length)*(i+0.5)} text={opt} />
                            {/each}
                        </g>
                    {/if}
                {/if}
            </g>

            <!-- triangle -->
            <polygon points="200 360 210 370 190 370"/>
        </svg>
    </div>
</div>

<script>
    import FullArc from "../components/FullArc.svelte";
    import ArcLabel from "../components/ArcLabel.svelte";
    import Arc from "../components/Arc.svelte";

    // ============================== input ==============================
    let elements = [];
    let input_value = "";
    let tick = 0;

    function clickAddElement() {
        elements = [...elements, input_value];
        angle = (360 / elements.length) / 2
        tick++;
        setTimeout(function() {
            tick++;
        }, 1);
        input_value = ""
    }

    function clickResetElement() {
        elements = []
        input_value = ""
    }

    // ============================== sphere element ==============================
    let r = 150;
    let angle = (360 / elements.length) / 2;
    let rolledOption = "";

    function randint(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min
    }

    function randfloat(min, max) {
      return Math.random() * (max - min) + min
    }

    function roundUp(x, z) {
      return Math.ceil(x / z) * z
    }

    function click() {
        console.log("click", angle);
        let roll = randint(0, elements.length-1)
        let rollPlace = randfloat(0.2*(360 / elements.length), 0.8*(360 / elements.length))
        let finalAngle = roll * (360 / elements.length) + rollPlace
        let spins = randint(2, 3)
        angle = roundUp(angle, 360) + spins * 360 + finalAngle
        rolledOption = elements[roll]
    }
    function transitionend() {
        console.log(rolledOption);
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

        input {
            border-width: 1px;
            border-radius: 8px;
            display: block;
            padding: 0.625rem;
            background-color: #374151;
            border-color: #4b5563;
            color: white;

            border-style: none;
            // scale: 0;
            &:focus {
                --ring-color: rgb(59 130 246);
                border-color: rgb(59 130 246);
            }
        }
        button {
            border-style: none;
            // inline-flex
            display: inline-flex;
            // items-center
            align-items: center;
            // px-5
            padding-left: 15px;
            padding-right: 15px;
            // py-2.5
            padding-top: 4px;
            padding-bottom: 4px;
            // text-sm
            font-size: 14px;
            line-height: 20px;
            // font-medium
            font-weight: 500;
            // text-center
            text-align: center;
            // text-white
            color: white;
            // rounded-lg
            border-radius: 8px;
            // dark:bg-blue-600
            background-color: #1C64F2;

            &:hover {
                // dark:hover:bg-blue-700
                background-color: #1d4ed8;

            }
            &:focus {
                // focus:ring-4
                box-shadow: var(--tw-ring-inset) 0 0 0 calc(4px + var(--tw-ring-offset-width)) var(--tw-ring-color);
                // focus:outline-none
                // dark:focus:ring-blue-800
                --ring-color: #1E40AF;
            }
        }
    }
}
:global(body) {
    background-color: rgb(17 24 39);
    color: #fff;
    margin: 0;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    padding-top: 60px;
    user-select: none;
}

svg {
  display: block;
}

polygon {
  fill: yellow;
}

#hello {
    transition: transform 3s ease-out;
}

</style>

