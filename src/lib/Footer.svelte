<script>
    export let logoSrc = "/images/footer_logo.png";
</script>

<footer>
    <div class="footer_bottom">
        <div class="social_icon">
            <ul class="list-unstyled">
                <li class="connect"><h4>Connect</h4></li>
                <li><a href="#"><i class="fa fa-facebook"></i></a></li>
                <li><a href="#"><i class="fa fa-twitter"></i></a></li>
                <li><a href="#"><i class="fa fa-youtube"></i></a></li>
                <li><a href="#"><i class="fa fa-safari"></i></a></li>
            </ul>
        </div>
        
        <img src={logoSrc} alt="Footer Logo" style="height: 80px; width: auto; margin-top: 20px;" />
        
        <h1 class="footer-showcase">WELLBEING~SVASTI</h1>
        
        <p>
            © 2025 Rutger Kortenhorst. All Rights Reserved | Design and Developed by
            <a href="#">Burning Desire Inclusive</a>
        </p>
    </div>
</footer>

<style>
/* Footer CSS from sanskrit.css */
footer { background-image: url("/images/footerimg.png") !important; border-top: 6px solid #383842; width: 100%; color: #cacaca; }
.footer_bottom { text-align: center; padding: 2em 0; background-image: url("/images/footerimg.png"); background-size: cover; }
.footer-showcase { font-size: 45px; margin: 10px 0; font-family: 'Edensor', 'Noto Sans Devanagari', sans-serif !important; color: #AEA17E; }
.social_icon ul { padding: 0; margin-bottom: 20px; }
.social_icon ul li { display: inline-block; margin: 0 5px; }
.social_icon ul li a i { width: 35px; height: 35px; line-height: 35px; border: 1px solid #fff; border-radius: 50%; text-align: center; color: #fff; transition: 0.3s; }
.social_icon ul li a i:hover { background: #55ad55; border-color: #55ad55; }
.connect h4 { color: #fff; display: inline-block; margin-right: 15px; font-size: 18px; }
a { color: #68b4a9; text-decoration: none; }
</style>