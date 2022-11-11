<script>
    import { onMount } from "svelte";
    
    onMount(() => {
        // Custom Cursor Selector
        const CUSTOM_CURSOR = document.querySelector('.cursor');

        // Custom Cursor Listener
        document.addEventListener('mousemove', (e) => 
            CUSTOM_CURSOR.style.cssText =`left: ${e.clientX - 11.5}px; top: ${e.clientY - 13}px;`, false
        );

        // Add event listeners for each btn class
        document.querySelectorAll(".btn").forEach((btn) => {
            // Button Position
            const POSITION = btn.getBoundingClientRect();

            // Mouse enter + move listener
            btn.addEventListener("mousemove", (e) => {
                // Modify Custom Cursor
                CUSTOM_CURSOR.classList.add("scale-150");
                CUSTOM_CURSOR.classList.add("bg-white");
            
                // Get the mouse x and y coords
                const X = e.pageX - POSITION.left - POSITION.width / 2;
                const Y = e.pageY - POSITION.top - POSITION.height / 2;

                // Move the text
                btn.children[0].style.transform = `translate(${X * 0.3}px, ${Y * 0.5}px)`;
            });
            
            // Mouse exit listener
            btn.addEventListener("mouseout", (_) => {
                // Modify Custom Cursor
                CUSTOM_CURSOR.classList.remove("scale-150");
                CUSTOM_CURSOR.classList.remove("bg-white");

                // Reset text to original postion
                btn.children[0].style.transform = "translate(0px, 0px)";
            });
        });
    });
</script>

<!-- Custom Cursor -->
<div class="cursor fixed pointer-events-none border-2 border-white p-[0.6rem] rounded-full mix-blend-difference z-10 ease-linear"></div>

<!-- Magnetic Text -->
<a href="/" class="btn rounded-2xl mt-20 border-white border-2 mx-96 font-black tracking-widest relative flex items-center justify-center cursor-pointer">
    <span class="relative ease-linear duration-200 text-white text-2xl p-20 tracking-widest">SIMPSON RESEARCH</span>
</a>
