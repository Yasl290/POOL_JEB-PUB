<script>
    import { onMount } from 'svelte';

    let email = '';
    let password = '';
    let rememberMe = false;
    let loading = false;
    let error = '';
    let mounted = false;

    onMount(() => {
        mounted = true;
    });

    async function handleSubmit() {
        if (!email || !password) {
            error = 'Veuillez remplir tous les champs';
            return;
        }

        loading = true;
        error = '';

        try {
            // Simulation d'appel API - à remplacer par votre API backend
            await new Promise(resolve => setTimeout(resolve, 1500));

            // Logique de connexion ici
            console.log('Connexion:', { email, password, rememberMe });

            // Redirection après connexion réussie
            // window.location.href = '/dashboard'; // ou utilisez goto de $app/navigation

        } catch (err) {
            error = 'Erreur de connexion. Vérifiez vos identifiants.';
        } finally {
            loading = false;
        }
    }

    function handleGoogleLogin() {
        console.log('Connexion Google');
        // Logique de connexion Google
    }

    function handleLinkedInLogin() {
        console.log('Connexion LinkedIn');
        // Logique de connexion LinkedIn
    }
</script>

<svelte:head>
    <title>Connexion - JEB Incubator</title>
    <meta name="description" content="Connectez-vous à votre espace JEB Incubator" />
</svelte:head>

<main class="login-page" class:mounted>
    <div class="login-container">
        <!-- Partie gauche - Image/Branding -->
        <div class="login-visual">
            <div class="visual-content">
                <div class="logo-section">
                    <div class="logo-icon">
                        <i class="fas fa-rocket"></i>
                    </div>
                    <h1 class="logo-text">JEB Incubator</h1>
                </div>

                <div class="visual-message">
                    <h2>Transformez vos idées en success stories</h2>
                    <p>Rejoignez notre écosystème d'innovation et accédez aux ressources exclusives de notre incubateur.</p>
                </div>

                <div class="visual-stats">
                    <div class="stat-item">
                        <span class="stat-number">150+</span>
                        <span class="stat-label">Startups</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-number">€50M</span>
                        <span class="stat-label">Levés</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-number">85%</span>
                        <span class="stat-label">Réussite</span>
                    </div>
                </div>
            </div>

            <!-- Éléments décoratifs -->
            <div class="floating-elements">
                <div class="floating-icon icon-1">
                    <i class="fas fa-lightbulb"></i>
                </div>
                <div class="floating-icon icon-2">
                    <i class="fas fa-chart-line"></i>
                </div>
                <div class="floating-icon icon-3">
                    <i class="fas fa-users"></i>
                </div>
            </div>
        </div>

        <!-- Partie droite - Formulaire -->
        <div class="login-form-section">
            <div class="form-container">
                <!-- Navigation retour -->
                <div class="back-nav">
                    <a href="/" class="back-link">
                        <i class="fas fa-arrow-left"></i>
                        <span>Retour à l'accueil</span>
                    </a>
                </div>

                <div class="form-header">
                    <h2>Connexion</h2>
                    <p>Accédez à votre espace personnel</p>
                </div>

                <!-- Connexions sociales -->
                <div class="social-login">
                    <button type="button" class="social-btn google-btn" on:click={handleGoogleLogin}>
                        <i class="fab fa-google"></i>
                        <span>Continuer avec Google</span>
                    </button>
                    <button type="button" class="social-btn linkedin-btn" on:click={handleLinkedInLogin}>
                        <i class="fab fa-linkedin"></i>
                        <span>Continuer avec LinkedIn</span>
                    </button>
                </div>

                <div class="divider">
                    <span>ou</span>
                </div>

                <!-- Formulaire de connexion -->
                <form on:submit|preventDefault={handleSubmit} class="login-form">
                    {#if error}
                        <div class="error-message">
                            <i class="fas fa-exclamation-triangle"></i>
                            <span>{error}</span>
                        </div>
                    {/if}

                    <div class="form-group">
                        <label for="email">Adresse e-mail</label>
                        <div class="input-wrapper">
                            <i class="fas fa-envelope"></i>
                            <input
                                    id="email"
                                    type="email"
                                    bind:value={email}
                                    placeholder="votre@email.com"
                                    required
                                    disabled={loading}
                            />
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="password">Mot de passe</label>
                        <div class="input-wrapper">
                            <i class="fas fa-lock"></i>
                            <input
                                    id="password"
                                    type="password"
                                    bind:value={password}
                                    placeholder="Votre mot de passe"
                                    required
                                    disabled={loading}
                            />
                        </div>
                    </div>

                    <div class="form-options">
                        <label class="checkbox-wrapper">
                            <input type="checkbox" bind:checked={rememberMe} disabled={loading} />
                            <span class="checkmark"></span>
                            <span class="checkbox-label">Se souvenir de moi</span>
                        </label>
                        <a href="/forgot-password" class="forgot-link">Mot de passe oublié ?</a>
                    </div>

                    <button type="submit" class="submit-btn" disabled={loading} class:loading>
                        {#if loading}
                            <i class="fas fa-spinner fa-spin"></i>
                            <span>Connexion...</span>
                        {:else}
                            <i class="fas fa-sign-in-alt"></i>
                            <span>Se connecter</span>
                        {/if}
                    </button>
                </form>

                <div class="form-footer">
                    <p>
                        Pas encore de compte ?
                        <a href="/register" class="register-link">Créer un compte</a>
                    </p>
                </div>
            </div>
        </div>
    </div>

    <!-- Formes décoratives -->
    <div class="bg-shapes">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
        <div class="shape shape-3"></div>
    </div>
</main>

<style>
    .login-page {
        min-height: 100vh;
        background: linear-gradient(135deg, #f8f9fa 0%, #eed5fb 50%, #e4bef8 100%);
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 2rem 1rem;
        position: relative;
        overflow: hidden;
        opacity: 0;
        transform: translateY(20px);
        transition: all 0.8s ease-out;
    }

    .login-page.mounted {
        opacity: 1;
        transform: translateY(0);
    }

    .login-container {
        width: 100%;
        max-width: 1200px;
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(20px);
        border-radius: 24px;
        box-shadow: 0 25px 80px rgba(0, 0, 0, 0.1);
        border: 1px solid rgba(241, 133, 133, 0.1);
        overflow: hidden;
        display: grid;
        grid-template-columns: 1fr 1fr;
        min-height: 600px;
        position: relative;
        z-index: 2;
    }

    /* Partie visuelle gauche */
    .login-visual {
        background: var(--primary-gradient);
        padding: 3rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        color: white;
        position: relative;
        overflow: hidden;
    }

    .visual-content {
        position: relative;
        z-index: 2;
    }

    .logo-section {
        margin-bottom: 2rem;
    }

    .logo-icon {
        width: 80px;
        height: 80px;
        background: rgba(255, 255, 255, 0.2);
        backdrop-filter: blur(10px);
        border-radius: 20px;
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 0 auto 1rem;
        animation: float 3s ease-in-out infinite;
    }

    .logo-icon i {
        font-size: 2.5rem;
        color: white;
    }

    .logo-text {
        font-size: 2.5rem;
        font-weight: 800;
        font-family: 'Montserrat', sans-serif;
        margin-bottom: 0;
    }

    .visual-message h2 {
        font-size: 1.8rem;
        margin-bottom: 1rem;
        font-weight: 700;
    }

    .visual-message p {
        font-size: 1.1rem;
        opacity: 0.9;
        line-height: 1.6;
        margin-bottom: 2rem;
    }

    .visual-stats {
        display: flex;
        gap: 2rem;
        justify-content: center;
    }

    .stat-item {
        text-align: center;
    }

    .stat-number {
        display: block;
        font-size: 1.8rem;
        font-weight: 800;
        font-family: 'Montserrat', sans-serif;
        margin-bottom: 0.25rem;
    }

    .stat-label {
        font-size: 0.9rem;
        opacity: 0.8;
    }

    .floating-elements {
        position: absolute;
        inset: 0;
        pointer-events: none;
    }

    .floating-icon {
        position: absolute;
        width: 60px;
        height: 60px;
        background: rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(10px);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 1px solid rgba(255, 255, 255, 0.2);
    }

    .floating-icon i {
        font-size: 1.5rem;
        color: rgba(255, 255, 255, 0.8);
    }

    .icon-1 {
        top: 20%;
        left: 10%;
        animation: float 4s ease-in-out infinite;
    }

    .icon-2 {
        top: 60%;
        right: 15%;
        animation: float 4s ease-in-out infinite 1s;
    }

    .icon-3 {
        bottom: 20%;
        left: 20%;
        animation: float 4s ease-in-out infinite 2s;
    }

    /* Partie formulaire droite */
    .login-form-section {
        padding: 3rem;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .form-container {
        width: 100%;
        max-width: 400px;
    }

    .back-nav {
        margin-bottom: 1.5rem;
    }

    .back-link {
        display: inline-flex;
        align-items: center;
        gap: 0.5rem;
        color: var(--gray);
        text-decoration: none;
        font-size: 0.9rem;
        font-weight: 500;
        transition: all 0.3s ease;
        padding: 0.5rem 0;
    }

    .back-link:hover {
        color: var(--coral);
        transform: translateX(-3px);
    }

    .form-header {
        text-align: center;
        margin-bottom: 2rem;
    }

    .form-header h2 {
        font-size: 2rem;
        color: var(--black);
        margin-bottom: 0.5rem;
        background: var(--primary-gradient);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
    }

    .form-header p {
        color: var(--gray);
        margin-bottom: 0;
    }

    .social-login {
        display: flex;
        flex-direction: column;
        gap: 0.75rem;
        margin-bottom: 1.5rem;
    }

    .social-btn {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 0.75rem;
        padding: 12px 16px;
        border: 1px solid #ddd;
        background: white;
        border-radius: 12px;
        font-weight: 600;
        transition: all 0.3s ease;
        cursor: pointer;
    }

    .social-btn:hover {
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
    }

    .google-btn {
        color: #db4437;
        border-color: #db4437;
    }

    .google-btn:hover {
        background: #db4437;
        color: white;
    }

    .linkedin-btn {
        color: #0077b5;
        border-color: #0077b5;
    }

    .linkedin-btn:hover {
        background: #0077b5;
        color: white;
    }

    .divider {
        position: relative;
        text-align: center;
        margin: 1.5rem 0;
    }

    .divider::before {
        content: '';
        position: absolute;
        top: 50%;
        left: 0;
        right: 0;
        height: 1px;
        background: #ddd;
    }

    .divider span {
        background: white;
        padding: 0 1rem;
        color: var(--gray);
        font-size: 0.9rem;
    }

    .login-form {
        display: flex;
        flex-direction: column;
        gap: 1.25rem;
    }

    .error-message {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        padding: 12px 16px;
        background: #fee;
        border: 1px solid #fcc;
        border-radius: 8px;
        color: #c33;
        font-size: 0.9rem;
    }

    .form-group {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
    }

    .form-group label {
        font-weight: 600;
        color: var(--black);
        font-size: 0.9rem;
    }

    .input-wrapper {
        position: relative;
    }

    .input-wrapper i {
        position: absolute;
        left: 16px;
        top: 50%;
        transform: translateY(-50%);
        color: var(--gray);
        font-size: 0.9rem;
    }

    .input-wrapper input {
        width: 100%;
        padding: 14px 16px 14px 45px;
        border: 1px solid #ddd;
        border-radius: 12px;
        font-size: 1rem;
        transition: all 0.3s ease;
        background: white;
    }

    .input-wrapper input:focus {
        outline: none;
        border-color: var(--coral);
        box-shadow: 0 0 0 3px rgba(241, 133, 133, 0.1);
    }

    .form-options {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0.5rem 0;
    }

    .checkbox-wrapper {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        cursor: pointer;
        font-size: 0.9rem;
    }

    .checkbox-wrapper input[type="checkbox"] {
        display: none;
    }

    .checkmark {
        width: 18px;
        height: 18px;
        border: 2px solid #ddd;
        border-radius: 4px;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: all 0.3s ease;
    }

    .checkbox-wrapper input[type="checkbox"]:checked + .checkmark {
        background: var(--coral);
        border-color: var(--coral);
    }

    .checkbox-wrapper input[type="checkbox"]:checked + .checkmark::after {
        content: '✓';
        color: white;
        font-size: 12px;
        font-weight: bold;
    }

    .forgot-link {
        color: var(--coral);
        font-size: 0.9rem;
        text-decoration: none;
        font-weight: 500;
    }

    .forgot-link:hover {
        text-decoration: underline;
    }

    .submit-btn {
        background: var(--primary-gradient);
        color: white;
        border: none;
        padding: 16px;
        border-radius: 12px;
        font-size: 1rem;
        font-weight: 600;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 0.5rem;
        cursor: pointer;
        transition: all 0.3s ease;
        box-shadow: 0 8px 25px rgba(241, 133, 133, 0.3);
    }

    .submit-btn:hover:not(:disabled) {
        transform: translateY(-2px);
        box-shadow: 0 12px 35px rgba(241, 133, 133, 0.4);
    }

    .submit-btn:disabled {
        opacity: 0.7;
        cursor: not-allowed;
    }

    .form-footer {
        text-align: center;
        margin-top: 1.5rem;
        padding-top: 1.5rem;
        border-top: 1px solid #eee;
    }

    .form-footer p {
        color: var(--gray);
        margin-bottom: 0;
    }

    .register-link {
        color: var(--coral);
        font-weight: 600;
        text-decoration: none;
    }

    .register-link:hover {
        text-decoration: underline;
    }

    /* Formes décoratives */
    .bg-shapes {
        position: absolute;
        inset: 0;
        pointer-events: none;
        z-index: 1;
    }

    .shape {
        position: absolute;
        border-radius: 50%;
        opacity: 0.05;
    }

    .shape-1 {
        width: 300px;
        height: 300px;
        background: var(--coral);
        top: -100px;
        right: -100px;
        animation: rotate 20s linear infinite;
    }

    .shape-2 {
        width: 200px;
        height: 200px;
        background: var(--deep-purple);
        bottom: -50px;
        left: -50px;
        animation: rotate 15s linear infinite reverse;
    }

    .shape-3 {
        width: 150px;
        height: 150px;
        background: var(--light-purple);
        top: 40%;
        left: -75px;
        animation: float 6s ease-in-out infinite;
    }

    @keyframes float {
        0%, 100% { transform: translateY(0px); }
        50% { transform: translateY(-10px); }
    }

    @keyframes rotate {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }

    /* Responsive */
    @media (max-width: 1024px) {
        .login-container {
            grid-template-columns: 1fr;
            max-width: 500px;
        }

        .login-visual {
            display: none;
        }

        .login-form-section {
            padding: 2rem;
        }

        .back-nav {
            margin-bottom: 1rem;
        }
    }

    @media (max-width: 768px) {
        .login-page {
            padding: 1rem;
        }

        .login-form-section {
            padding: 1.5rem;
        }

        .form-container {
            max-width: 100%;
        }

        .visual-stats {
            flex-direction: column;
            gap: 1rem;
        }
    }

    @media (max-width: 480px) {
        .social-login {
            gap: 0.5rem;
        }

        .social-btn {
            padding: 10px 12px;
            font-size: 0.9rem;
        }

        .form-options {
            flex-direction: column;
            align-items: flex-start;
            gap: 0.75rem;
        }
    }
</style>