<div class="navbar" class:dropdown>
  <div class="wrapper" class:dropdown>
    <div>
      <div class="burger-menu">
        <NavElement icon="fas fa-bars" on:click={dropdownNav}>Menu</NavElement>
      </div>
      <div class="nav-section" class:dropdown>
        <!-- on:click required to close dropdown again -->
        <NavElement icon="fas fa-cogs" link="/manage/{guildId}/settings" on:click={closeDropdown}>Settings</NavElement>
        <NavElement icon="fas fa-copy" link="/manage/{guildId}/transcripts" on:click={closeDropdown}>Transcripts</NavElement>
        <NavElement icon="fas fa-mouse-pointer" link="/manage/{guildId}/panels" on:click={closeDropdown}>Reaction Panels</NavElement>
        <NavElement icon="fas fa-users" link="/manage/{guildId}/teams" on:click={closeDropdown}>Teams</NavElement>
        <NavElement icon="fas fa-ticket-alt" link="/manage/{guildId}/tickets" on:click={closeDropdown}>Tickets</NavElement>
        <NavElement icon="fas fa-ban" link="/manage/{guildId}/blacklist" on:click={closeDropdown}>Blacklist</NavElement>
        <NavElement icon="fas fa-tags" link="/manage/{guildId}/tags" on:click={closeDropdown}>Tags</NavElement>
      </div>
    </div>
    <div>
      <div class="nav-section" class:dropdown>
        <NavElement icon="fas fa-server" link="/#">Servers</NavElement>
        <NavElement icon="fas fa-sign-out-alt" link="/logout">Logout</NavElement>
      </div>
    </div>
  </div>
</div>

<script>
    export let guildId;
    export let dropdown = false;

    import NavElement from "../components/NavElement.svelte";

    function dropdownNav() {
        dropdown = !dropdown;
    }

    function closeDropdown() {
        dropdown = false;
    }
</script>

<style>
    .navbar {
        display: flex;
        justify-content: center;
        width: 100%;
        background-color: #272727;
    }

    .wrapper {
        display: flex;
        width: 98%;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }

    .nav-section {
        display: flex;
        flex-direction: row;
    }

    .burger-menu {
        display: none;
    }

    @media only screen and (max-width: 950px) {
        .nav-section {
            display: none;
        }

        .burger-menu {
            display: flex;
        }

        .nav-section.dropdown {
            display: flex;
            flex-direction: column;
        }

        .wrapper {
            flex-direction: column;
            align-items: flex-start;
            overflow: hidden;
        }

        .dropdown {
            transition-property: height;
        }

        .navbar {
            position: relative;
            height: 49px;
            transition: all .3s ease-in-out;
            overflow: hidden;
        }

        .navbar.dropdown, .wrapper.dropdown {
            height: 100%;
            overflow: hidden;
        }

        .wrapper.dropdown {
            position: absolute;
        }

        :global(.nav-element) {
            padding: 15px 0 10px 15px !important;
        }

        :global(.super-container.dropdown) {
            display: none;
        }
    }
</style>
