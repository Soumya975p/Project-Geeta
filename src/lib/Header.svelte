<script>
  let activeDropdown = null;

  function show(menu) { activeDropdown = menu; }
  function hide() { activeDropdown = null; }
</script>

<header class="nav_background">
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container nav-container">
      <a class="navbar-brand" href="/">
        <img src="/images/logo.png" alt="Logo" />
      </a>
      
      <button class="navbar-toggler" type="button">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse">
        <ul class="navbar-nav ml-auto mt-2 mt-lg-0">
          <li class="nav-item active">
            <a class="nav-link" href="search.php"><i class="fa fa-search"></i></a>
          </li>

          <li class="nav-item dropdown" 
              on:mouseenter={() => show('ayurveda')} 
              on:mouseleave={hide}>
            <a class="nav-link dropdown-toggle" href="#">ĀYURVEDA</a>
            <div class="dropdown-menu" class:show={activeDropdown === 'ayurveda'}>
              <a class="dropdown-item" href="#">Introduction</a>
              <a class="dropdown-item" href="#">Timing</a>
              <a class="dropdown-item" href="#">Food</a>
            </div>
          </li>

          <li class="nav-item dropdown" 
              on:mouseenter={() => show('yoga')} 
              on:mouseleave={hide}>
            <a class="nav-link dropdown-toggle" href="#">YOGASŪTRAS</a>
            <div class="dropdown-menu" class:show={activeDropdown === 'yoga'}>
              <a class="dropdown-item" href="#">Introduction</a>
              <a class="dropdown-item" href="#">Obstacles</a>
              <a class="dropdown-item" href="#">Practices</a>
              <a class="dropdown-item" href="#">Yogāsana</a>
              <a class="dropdown-item" href="#">Glossary</a>
            </div>
          </li>

          <li class="nav-item dropdown"
              on:mouseenter={() => show('gita')} 
              on:mouseleave={hide}>
            <a class="nav-link active" href="#">BHAGAVAD GĪTĀ</a>
             <div class="dropdown-menu" class:show={activeDropdown === 'gita'}>
              <a class="dropdown-item" href="#">Introduction</a>
              <a class="dropdown-item" href="#">Timing</a>
              <a class="dropdown-item" href="#">Obstacles</a>
              <a class="dropdown-item" href="#">Practices</a>
              <a class="dropdown-item" href="#">Glossary</a>
            </div>
          </li>

          <li class="nav-item dropdown"
              on:mouseenter={() => show('upanisads')} 
              on:mouseleave={hide}>
            <a class="nav-link dropdown-toggle" href="#">UPANIṢADS</a>
            <div class="dropdown-menu" class:show={activeDropdown === 'upanisads'}>
              <a class="dropdown-item" href="#">ĪŚOPANIṢAD</a>
              <a class="dropdown-item" href="#">TAITTIRĪYOPANIṢAD</a>
              <a class="dropdown-item" href="#">MĀṆḌŪKYOPANIṢAD</a>
              <a class="dropdown-item" href="#">KENOPANIṢAD</a>
              <a class="dropdown-item" href="#">KAṬHOPANIṢAD</a>
              <a class="dropdown-item" href="#">AITAREYOPANIṢAD</a>
              <a class="dropdown-item" href="#">MUṆḌAKOPANIṢAD</a>
              <a class="dropdown-item" href="#">PRAŚNOPANIṢAD</a>
            </div>
          </li>

          <li class="nav-item dropdown"
              on:mouseenter={() => show('sanskrit')} 
              on:mouseleave={hide}>
            <a class="nav-link dropdown-toggle" href="#">SANSKRIT</a>
            <div class="dropdown-menu" class:show={activeDropdown === 'sanskrit'}>
              <a class="dropdown-item" href="#">Devotional Songs</a>
              <a class="dropdown-item" href="#">Grammar Songs</a>
              <a class="dropdown-item" href="#">Fun Songs</a>
              <a class="dropdown-item" href="#">Script Songs</a>
            </div>
          </li>

          <li class="nav-item">
            <a class="nav-link" href="#">CONTACT US</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</header>

<style>
/* CSS extracted from your sanskrit.css */
.nav_background .bg-light {
    background: #ffffff !important;
    position: absolute;
    padding: 6px 0;
    width: 100%;
    z-index: 999;
}
.nav_background .navbar-brand img { width: 60%; }
.nav_background .navbar-light .navbar-nav .nav-link {
    color: #3E4939;
    text-align: center;
    font-size: 12px;
    font-weight: 500;
    text-transform: uppercase;
}
.nav_background .navbar-light .navbar-nav .nav-link:hover, .nav_background .navbar-light .navbar-nav .active > .nav-link {
    color: burlywood;
}
.dropdown-menu {
    border-radius: .25rem;
    padding: .5rem 0;
    margin: .125rem 0 0;
    border: 1px solid rgba(0,0,0,.15);
}
.dropdown-item {
    padding: .25rem 1.5rem;
    font-weight: 400;
    color: #000;
    line-height: 2;
}
.dropdown-item:hover {
    background-color: #f8f9fa;
    color: #bd003c;
}
</style>