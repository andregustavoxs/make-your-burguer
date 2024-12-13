<template>
    <footer id="footer">
        <div class="footer-content">
            <div class="footer-section">
                <h3>Make Your Burger</h3>
                <p>Crie o hambúrguer dos seus sonhos com os melhores ingredientes!</p>
            </div>
            <div class="footer-section">
                <h4>Links Rápidos</h4>
                <nav>
                    <router-link to="/">Home</router-link>
                    <router-link to="/pedidos">Pedidos</router-link>
                </nav>
            </div>
            <div class="footer-section">
                <h4>Contato</h4>
                <p>
                    <i class="fas fa-phone"></i> (11) 99999-9999<br>
                    <i class="fas fa-envelope"></i> contato@makeyourburger.com
                </p>
            </div>
        </div>
        <div class="footer-bottom">
            <p>Make Your Burger &copy; {{ currentYear }} - Todos os direitos reservados</p>
        </div>
    </footer>
</template>

<script>
export default {
    name: "Footer",
    computed: {
        currentYear() {
            return new Date().getFullYear();
        }
    }
}
</script>

<style scoped>
#footer {
    background-color: #222;
    border-top: 4px solid #FCBA03;
    color: #fff;
    padding: 0;
    width: 100%;
}

.footer-content {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
}

.footer-section {
    padding: 1rem;
}

.footer-section h3 {
    color: #FCBA03;
    font-size: 1.5rem;
    margin-bottom: 1rem;
    font-weight: 600;
}

.footer-section h4 {
    color: #FCBA03;
    font-size: 1.2rem;
    margin-bottom: 1rem;
    font-weight: 600;
}

.footer-section p {
    color: #ccc;
    line-height: 1.6;
    margin-bottom: 1rem;
}

.footer-section nav {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.footer-section a {
    color: #ccc;
    text-decoration: none;
    transition: all 0.3s ease;
    display: inline-block;
    padding: 0.3rem 0;
}

.footer-section a:hover {
    color: #FCBA03;
    transform: translateX(5px);
}

.footer-section i {
    color: #FCBA03;
    margin-right: 0.5rem;
    width: 20px;
}

.footer-bottom {
    background-color: rgba(0, 0, 0, 0.2);
    padding: 1rem;
    text-align: center;
    font-size: 0.9rem;
}

.footer-bottom p {
    color: #888;
    margin: 0;
}

@media (max-width: 768px) {
    .footer-content {
        grid-template-columns: 1fr;
        text-align: center;
        gap: 1rem;
    }

    .footer-section nav {
        align-items: center;
    }

    .footer-section a:hover {
        transform: none;
    }
}
</style>
