<script lang="ts">
    import { onMount } from "svelte";


function addToEquation(value: string) {
        equation += value;
    }

    function backspace() {
        switch (equation.substring(equation.length - 3, equation.length)) {
            case " + ":
            case " * ":
            case " - ":
            case " / ":
                equation = equation.substring(0, equation.length - 3);
                break;
            default:
                equation = equation.substring(0, equation.length - 1);
        }
    }

    function clear() {
        equation = "";
    }

    function solve() {
        try {
            let answer = eval(equation);
            if (answer == undefined) throw SyntaxError;
            equation = answer;
        } catch (error) {
            let output = document.getElementById("output");
            output?.classList.add("bg-red-500");
            setTimeout(() => {
                output?.classList.remove("bg-red-500");
            }, 500);
        }
    }

    let equation: string = "";

    function onKeyDown(e: KeyboardEvent) {
        let button = document.getElementById(e.key);
        button?.click();
        button?.focus();
        setTimeout(() => {
            // @ts-ignore
            document.activeElement?.blur();
        }, 100);
    }

    onMount(() => {
        let allButtons = document.getElementsByTagName('button');
        for (let i = 0; i < allButtons.length; i++) {
            allButtons[i].addEventListener('click', () => {
                new Audio('/click.wav').play();
                document.activeElement?.blur();
            });
        }
    });
</script>

<svelte:head>
    <title>
        الة حاسبة
    </title>
    
</svelte:head>

<svelte:window on:keydown|preventDefault={onKeyDown} />

<div class="bg-[rgb(254,254,254)] min-h-[25rem] w-[17rem] rounded-3xl grid grid-cols-4 gap-2 p-4 shadow-2xl max-w-[17rem] ">
    <div id="output"
    class="bg-[#2386fe] rounded-full col-span-4 h-14 flex items-center pxl-4 pl-4 mb-1 text-2xl font-semibold shadow-xl text-white truncate ... transition-all select-none ">
        {equation}
    </div>
    <button id="Delete" on:click={() => clear()} class="bg-[#f3f6fd] hover:bg-[#f3f6fd]/110">AC</button>
    <button id="Backspace" on:click={() => backspace()} class="bg-[#f3f6fd] hover:bg-[#f3f6fd]/110 ">
        <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M22 3H7c-.69 0-1.23.35-1.59.88L0 12l5.41 8.11c.36.53.9.89 1.59.89h15a2 2 0 0 0 2-2V5a2 2 0 0 0-2-2m-3 12.59L17.59 17L14 13.41L10.41 17L9 15.59L12.59 12L9 8.41L10.41 7L14 10.59L17.59 7L19 8.41L15.41 12"/></svg>
    </button>
    <button id="%" on:click={() => addToEquation('/100')} class="bg-[#f3f6fd] hover:bg-[#f3f6fd]/110 ">
        <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="m18.5 3.5l2 2l-15 15l-2-2zM7 4c1.66 0 3 1.34 3 3s-1.34 3-3 3s-3-1.34-3-3s1.34-3 3-3m10 10c1.66 0 3 1.34 3 3s-1.34 3-3 3s-3-1.34-3-3s1.34-3 3-3M7 6c-.55 0-1 .45-1 1s.45 1 1 1s1-.45 1-1s-.45-1-1-1m10 10c-.55 0-1 .45-1 1s.45 1 1 1s1-.45 1-1s-.45-1-1-1"/></svg>
    </button>
    <button id="+" on:click={() => addToEquation(' + ')} class="bg-[#63dd75] text-[#f6f8f9] hover:bg-[#63dd75]/80"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M20 14h-6v6h-4v-6H4v-4h6V4h4v6h6z"/></svg></button>

    <button id="7" on:click={() => addToEquation('7')}>7</button>
    <button id="8" on:click={() => addToEquation('8')}>8</button>
    <button id="9" on:click={() => addToEquation('9')}>9</button>
    <button id="-" on:click={() => addToEquation(' - ')}  class="bg-[#fe4459] text-[#f6f8f9] hover:bg-[#fe4459]/80"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M20 14H4v-4h16"/></svg></button>
    <button id="4" on:click={() => addToEquation('4')}>4</button>
    <button  id="5" on:click={() => addToEquation('5')}>5</button>
    <button id="6" on:click={() => addToEquation('6')}>6</button>
    <button id="/" on:click={() => addToEquation(' / ')} class="bg-[#1e88fc] text-[#f6f8f9] hover:bg-[#1e88fc]/80"><svg xmlns="http://www.w3.org/2000/svg"  class="h-7 w-7" viewBox="0 0 24 24"><path fill="currentColor" d="M19 13H5v-2h14zm-7-8a2 2 0 0 1 2 2a2 2 0 0 1-2 2a2 2 0 0 1-2-2a2 2 0 0 1 2-2m0 10a2 2 0 0 1 2 2a2 2 0 0 1-2 2a2 2 0 0 1-2-2a2 2 0 0 1 2-2"/></svg></button>
    <button id="1" on:click={() => addToEquation('1')}>1</button>
    <button id="2" on:click={() => addToEquation('2')}>2</button>
    <button id="3" on:click={() => addToEquation('3')}>3</button>
    <button id="*" on:click={() => addToEquation(' * ')} class="bg-[#fdc704] text-[#f6f8f9] hover:bg-[#fdc704]/80"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M20 6.91L17.09 4L12 9.09L6.91 4L4 6.91L9.09 12L4 17.09L6.91 20L12 14.91L17.09 20L20 17.09L14.91 12z"/></svg></button>
    <button id="." on:click={() => addToEquation('.')}>.</button>
    <button id="0" on:click={() => addToEquation('0')}>0</button>
    <button id="=" on:click={() => solve()} class=" col-span-2 bg-[#f3f6fc] "><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><path fill="currentColor" d="M19 10H5V8h14zm0 6H5v-2h14z"/></svg></button>
</div>
