<script>
  import { onMount } from "svelte";

  let display = "0";
  let currentNumber = "";
  let previousNumber = "";
  let operation = null;
  let theme = 1;

  function handleNumber(num) {
    if (display === "0" || display === "Error") {
      display = num;
    } else {
      display += num;
    }
    currentNumber = display;
  }

  function handleOperation(op) {
    previousNumber = currentNumber;
    operation = op;
    display = "0";
  }

  function calculate() {
    if (!previousNumber || !currentNumber || !operation) return;

    const prev = parseFloat(previousNumber);
    const current = parseFloat(currentNumber);
    let result;

    switch (operation) {
      case "+":
        result = prev + current;
        break;
      case "-":
        result = prev - current;
        break;
      case "x":
        result = prev * current;
        break;
      case "/":
        if (current === 0) {
          display = "Error";
          return;
        }
        result = prev / current;
        break;
    }

    display = result.toString();
    currentNumber = result.toString();
    previousNumber = "";
    operation = null;
  }

  function reset() {
    display = "0";
    currentNumber = "";
    previousNumber = "";
    operation = null;
  }

  function del() {
    if (display.length === 1) {
      display = "0";
    } else {
      display = display.slice(0, -1);
    }
    currentNumber = display;
  }

  function toggleTheme() {
    theme = theme === 3 ? 1 : theme + 1;
    document.body.setAttribute("data-theme", `theme-${theme}`);
  }

  onMount(() => {
    document.body.setAttribute("data-theme", "theme-1");
  });
</script>

<main>
  <div class="calculator">
    <header>
      <h1>Calculator</h1>
      <div class="theme-switcher">
        <span>THEME</span>
        <div class="theme-toggle">
          <div class="numbers">
            <span>1</span>
            <span>2</span>
            <span>3</span>
          </div>
          <button on:click={toggleTheme}>
            <div class="slider">
              <div class="thumb" style="--position: {theme}"></div>
            </div>
          </button>
        </div>
      </div>
    </header>

    <div class="display">{display}</div>

    <div class="keypad">
      <button on:click={() => handleNumber("7")}>7</button>
      <button on:click={() => handleNumber("8")}>8</button>
      <button on:click={() => handleNumber("9")}>9</button>
      <button class="del" on:click={del}>DEL</button>
      <button on:click={() => handleNumber("4")}>4</button>
      <button on:click={() => handleNumber("5")}>5</button>
      <button on:click={() => handleNumber("6")}>6</button>
      <button on:click={() => handleOperation("+")}>+</button>
      <button on:click={() => handleNumber("1")}>1</button>
      <button on:click={() => handleNumber("2")}>2</button>
      <button on:click={() => handleNumber("3")}>3</button>
      <button on:click={() => handleOperation("-")}>-</button>
      <button on:click={() => handleNumber(".")}>.</button>
      <button on:click={() => handleNumber("0")}>0</button>
      <button on:click={() => handleOperation("/")}>/</button>
      <button on:click={() => handleOperation("x")}>x</button>
      <button class="span-2 reset" on:click={reset}>RESET</button>
      <button class="span-2 equals" on:click={calculate}>=</button>
    </div>
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    font-family: "League Spartan", sans-serif;
    min-height: 100vh;
    display: grid;
    place-items: center;
  }

  :global(body[data-theme="theme-1"]) {
    --main-bg: hsl(222, 26%, 31%);
    --keypad-bg: hsl(223, 31%, 20%);
    --screen-bg: hsl(224, 36%, 15%);
    --key-bg: hsl(30, 25%, 89%);
    --key-shadow: hsl(28, 16%, 65%);
    --key-text: hsl(221, 14%, 31%);
    --special-key-bg: hsl(225, 21%, 49%);
    --special-key-shadow: hsl(224, 28%, 35%);
    --equals-key-bg: hsl(6, 63%, 50%);
    --equals-key-shadow: hsl(6, 70%, 34%);
    --text: hsl(0, 0%, 100%);
  }

  :global(body[data-theme="theme-2"]) {
    --main-bg: hsl(0, 0%, 90%);
    --keypad-bg: hsl(0, 5%, 81%);
    --screen-bg: hsl(0, 0%, 93%);
    --key-bg: hsl(45, 7%, 89%);
    --key-shadow: hsl(35, 11%, 61%);
    --key-text: hsl(60, 10%, 19%);
    --special-key-bg: hsl(185, 42%, 37%);
    --special-key-shadow: hsl(185, 58%, 25%);
    --equals-key-bg: hsl(25, 98%, 40%);
    --equals-key-shadow: hsl(25, 99%, 27%);
    --text: hsl(60, 10%, 19%);
  }

  :global(body[data-theme="theme-3"]) {
    --main-bg: hsl(268, 75%, 9%);
    --keypad-bg: hsl(268, 71%, 12%);
    --screen-bg: hsl(268, 71%, 12%);
    --key-bg: hsl(268, 47%, 21%);
    --key-shadow: hsl(290, 70%, 36%);
    --key-text: hsl(52, 100%, 62%);
    --special-key-bg: hsl(281, 89%, 26%);
    --special-key-shadow: hsl(285, 91%, 52%);
    --equals-key-bg: hsl(176, 100%, 44%);
    --equals-key-shadow: hsl(177, 92%, 70%);
    --text: hsl(52, 100%, 62%);
  }

  :global(body) {
    background-color: var(--main-bg);
    color: var(--text);
  }

  .calculator {
    width: 100%;
    max-width: 540px;
    padding: 2rem;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
  }

  h1 {
    margin: 0;
    font-size: 2rem;
  }

  .theme-switcher {
    display: flex;
    align-items: end;
    gap: 1rem;
  }

  .theme-toggle {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
  }

  .numbers {
    display: flex;
    justify-content: space-around;
    padding: 0 0.25rem;
  }

  .slider {
    width: 4.5rem;
    height: 1.5rem;
    background: var(--keypad-bg);
    border-radius: 1rem;
    position: relative;
    padding: 0.25rem;
  }

  .thumb {
    width: 1rem;
    height: 1rem;
    background: var(--equals-key-bg);
    border-radius: 50%;
    position: absolute;
    left: calc((100% - 1.5rem) * (var(--position) - 1) / 2 + 0.25rem);
    transition: left 0.3s ease;
  }

  .display {
    background: var(--screen-bg);
    padding: 2rem;
    text-align: right;
    font-size: 2.5rem;
    border-radius: 0.5rem;
    margin-bottom: 1.5rem;
    min-height: 2.5rem;
  }

  .keypad {
    background: var(--keypad-bg);
    padding: 1.5rem;
    border-radius: 0.5rem;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
  }

  button {
    font-family: inherit;
    font-size: 1.5rem;
    padding: 1rem;
    border: none;
    border-radius: 0.5rem;
    background: var(--key-bg);
    color: var(--key-text);
    box-shadow: 0 4px var(--key-shadow);
    cursor: pointer;
    transition: transform 0.1s;
  }

  button:active {
    transform: translateY(2px);
  }

  .del,
  .reset {
    background: var(--special-key-bg);
    color: white;
    box-shadow: 0 4px var(--special-key-shadow);
    font-size: 1.25rem;
  }

  .equals {
    background: var(--equals-key-bg);
    color: white;
    box-shadow: 0 4px var(--equals-key-shadow);
  }

  .span-2 {
    grid-column: span 2;
  }
</style>
