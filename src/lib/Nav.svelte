<script>
    let navOpen = false;
    
    function handleNav() {
        navOpen = !navOpen;
    }
        
    function handleNavWithKey(e) {
        // console.log(e.code);
        if (e.code === "F1") {
            navOpen = !navOpen;
        }
    }	
</script>

<div id="mySidenav" class="sidenav" class:open={navOpen}>
    <button class="closebtn navbtn" on:click={handleNav}>&times;</button>
    <button class="navbtn">About</button>
    <button class="navbtn">Services</button>
    <button class="navbtn">Clients</button>
    <button class="navbtn">Contact</button>
</div>

<!-- Use Menu Icon to open the sidenav -->
<div class="navContainer" class:change={navOpen} on:click={handleNav} on:keydown={handleNavWithKey}>
    <div class="bar1"></div>
    <div class="bar2"></div>
    <div class="bar3"></div>
</div>
<svelte:window on:keydown={handleNavWithKey} />

<style>
    /* Hamburger Menu icon */	
    .navContainer {
        position: absolute;
        left: 0;
        display: inline-block;
        cursor: pointer;
    }
    
    .bar1, .bar2, .bar3 {
        width: 35px;
        height: 5px;
        background-color: #333;
        margin: 6px 0;
        transition: 0.4s;
    }
    
    .change .bar1 {
        -webkit-transform: rotate(-45deg) translate(-9px, 6px);
        transform: rotate(-45deg) translate(-9px, 6px);
    }
    
    .change .bar2 {opacity: 0;}
    
    .change .bar3 {
        -webkit-transform: rotate(45deg) translate(-8px, -8px);
        transform: rotate(45deg) translate(-8px, -8px);
    }
        
    /* The side navigation menu */
    .sidenav {
        height: 100%; 
        width: 0; /* 0 width - change this with JavaScript */
        position: fixed;
        z-index: 1;
        top: 0;
        left: 0;
        background-color: #111; 
        overflow-x: hidden; /* Disable horizontal scroll */
        padding-top: 60px;
        transition: 0.5s;
    }
    
    /* The navigation menu links */
    .sidenav button {
        padding: auto;
        text-decoration: none;
        font-size: 25px;
        color: #818181;
        display: block;
        transition: 0.3s;
    }
 
    /* When you mouse over the navigation links, change their color */
    .sidenav button:hover {
        color: #f1f1f1;
    }
    
    /* Position and style the close button (top right corner) */
    .sidenav .closebtn {
        position: absolute;
        top: 0;
        right: 25px;
        font-size: 36px;
        margin-left: 50px;
        color: white;
        padding: 0;
    }
    
    .navbtn {
        background: none;
        border: none;
        cursor: pointer;
        outline: inherit;
    }
    
    .open {
        width: 20%;
    }	
    
    /* On smaller screens, where height is less than 450px, change the style of the sidenav (less padding and a smaller font size) */
    @media screen and (max-height: 450px) {
      .sidenav {padding-top: 15px;}
      .sidenav button {font-size: 18px;}
    }
</style>