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
            <RouletteWheel
              r={150}
              options={options}
              onRolled={onRolled}
            />
          </g>
          <polygon points="200 360 210 370 190 370"/>
        </svg>
      </div>
</div>

<script>
    import RouletteWheel from "../components/RouletteWheel.svelte"
    let options = [];
    let asd = 0;
    let input_value = 0;

    function onRolled(opt) {
        console.log(opt)
    }
    function onClickTopic() {
        options = [...options, asd++];
        asd++;
        console.log(111);
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
