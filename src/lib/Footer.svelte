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
        
        <img src={logoSrc} alt="Footer Logo" style="height: 100px; width: auto; margin: 5px 0;" />
        
        <h1 class="footer-showcase">WELLBEING~SVASTI</h1>
        
        <p>
            © 2025 Rutger Kortenhorst. All Rights Reserved | Design and Developed by
            <a href="#">Burning Desire Inclusive</a>
        </p>
    </div>
</footer>

<style>
/* Footer CSS from sanskrit.css */
footer { 
    background-image: url("/images/footerimg.png") !important; 
    border-top: 6px solid #383842; 
    width: 100%; 
    color: #cacaca; 
    min-height: 180px;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
.footer_bottom { 
    text-align: center; 
    padding: 0.8em 0; 
    background-image: url("/images/footerimg.png"); 
    background-size: cover; 
    background-position: center;
    background-repeat: no-repeat;
    min-height: 180px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.footer-showcase { font-size: 36px; margin: 5px 0; font-family: 'Edensor', 'Noto Sans Devanagari', sans-serif !important; color: #AEA17E; }
.social_icon ul { padding: 0; margin-bottom: 8px; margin-top: 0; }
.social_icon ul li { display: inline-block; margin: 0 5px; }
.social_icon ul li a i { width: 32px; height: 32px; line-height: 32px; border: 1px solid #fff; border-radius: 50%; text-align: center; color: #fff; transition: 0.3s; font-size: 14px; }
.social_icon ul li a i:hover { background: #55ad55; border-color: #55ad55; }
.connect h4 { 
    color: #fff; 
    display: inline-block; 
    margin-right: 15px; 
    font-size: 18px; 
    margin: 0;
    font-family: 'edensor', 'Noto Sans Devanagari', sans-serif !important;
}
a { color: #68b4a9; text-decoration: none; }
.footer_bottom p { margin: 5px 0; font-size: 14px; }
</style>