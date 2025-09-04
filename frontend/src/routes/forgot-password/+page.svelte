<script>
    import { onMount } from 'svelte';

    let email = '';
    let loading = false;
    let success = false;
    let error = '';
    let mounted = false;

    onMount(() => {
        mounted = true;
    });

    async function handleSubmit() {
        if (!email) {
            error = 'Veuillez saisir votre adresse e-mail';
            return;
        }

        loading = true;
        error = '';

        try {
            // Simulation d'appel API
            await new Promise(resolve => setTimeout(resolve, 2000));

            console.log('Reset password for:', email);
            success = true;

        } catch (err) {
            error = 'Une erreur est survenue. Veuillez réessayer.';
        } finally {
            loading = false;
        }
    }

    function resetForm() {
        email = '';
        success = false;
        error = '';
    }
</script>

<svelte:head>
    <title>Mot de passe oublié - JEB Incubator</title>
    <meta name="description" content="Réinitialisez votre mot de passe JEB Incubator" />
</svelte:head>

<main class="forgot-password-page" class:mounted>
    <div class="page-container">
        <div class="content-wrapper">
            <!-- Retour vers la connexion -->
            <div class="back-nav">
                <a href="/login" class="back-link">
                    <i class="fas fa-arrow-left"></i>
                    <span>Retour à la connexion</span>
                </a>
            </div>

            <!-- Logo -->
            <div class="logo-section">
                <div class="logo-icon">
                    <i class="fas fa-rocket"></i>
                </div>
                <h1 class="logo-text">JEB Incubator</h1>
            </div>

            <div class="form-container">
                {#if !success}
                    <!-- Formulaire de récupération -->
                    <div class="form-header">
                        <h2>Mot de passe oublié ?</h2>
                        <p>Pas de problème ! Saisissez votre adresse e-mail et nous vous enverrons un lien pour réinitialiser votre mot de passe.</p>
                    </div>

                    <form on:submit|preventDefault={handleSubmit} class="forgot-form">
                        {#if error}
                            <div class="error-message" role="alert">
                                <i class="fas fa-exclamation-triangle"></i>
                                <span>{error}</span>
                            </div>
                        {/if}

                        <div class="form-group">
                            <label for="reset-email">Adresse e-mail</label>
                            <div class="input-wrapper">
                                <i class="fas fa-envelope" aria-hidden="true"></i>
                                <input
                                        id="reset-email"
                                        type="email"
                                        bind:value={email}
                                        placeholder="votre@email.com"
                                        required
                                        disabled={loading}
                                        autocomplete="email"
                                />
                            </div>
                        </div>

                        <button type="submit" class="submit-btn" disabled={loading} class:loading>
                            {#if loading}
                                <i class="fas fa-spinner fa-spin" aria-hidden="true"></i>
                                <span>Envoi en cours...</span>
                            {:else}
                                <i class="fas fa-paper-plane" aria-hidden="true"></i>
                                <span>Envoyer le lien</span>
                            {/if}
                        </button>
                    </form>
                {:else}
                    <!-- Message de succès -->
                    <div class="success-container">
                        <div class="success-icon">
                            <i class="fas fa-check-circle"></i>
                        </div>
                        <h2>E-mail envoyé !</h2>
                        <p>
                            Nous avons envoyé un lien de réinitialisation à <strong>{email}</strong>.
                            Vérifiez votre boîte de réception et vos spams.
                        </p>
                        <div class="success-actions">
                            <button type="button" class="btn-secondary" on:click={resetForm}>
                                <i class="fas fa-redo"></i>
                                <span>Essayer une autre adresse</span>
                            </button>
                            <a href="/login" class="btn-primary">
                                <i class="fas fa-sign-in-alt"></i>
                                <span>Retour à la connexion</span>
                            </a>
                        </div>
                    </div>
                {/if}

                <!-- Aide supplémentaire -->
                <div class="help-section">
                    <p class="help-text">
                        Vous n'arrivez toujours pas à vous connecter ?
                    </p>
                    <a href="/contact" class="help-link">
                        <i class="fas fa-life-ring"></i>
                        <span>Contactez le support</span>
                    </a>
                </div>
            </div>
        </div>

        <!-- Élément décoratif -->
        <div class="decorative-elements">
            <div class="floating-shape shape-1">
                <i class="fas fa-key"></i>
            </div>
            <div class="floating-shape shape-2">
                <i class="fas fa-lock"></i>
            </div>
            <div class="floating-shape shape-3">
                <i class="fas fa-shield-alt"></i>
            </div>
        </div>
    </div>

    <!-- Formes d'arrière-plan -->
    <div class="bg-shapes">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
    </div>
</main>

<style>
    .forgot-password-page {
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

    .forgot-password-page.mounted {
        opacity: 1;
        transform: translateY(0);
    }

    .page-container {
        width: 100%;
        max-width: 500px;
        position: relative;
        z-index: 2;
    }

    .content-wrapper {
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(20px);
        border-radius: 24px;
        padding: 2.5rem;
        box-shadow: 0 25px 80px rgba(0, 0, 0, 0.1);
        border: 1px solid rgba(241, 133, 133, 0.1);
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

    .logo-section {
        text-align: center;
        margin-bottom: 2rem;
    }

    .logo-icon {
        width: 70px;
        height: 70px;
        background: var(--primary-gradient);
        border-radius: 18px;
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 0 auto 1rem;
        box-shadow: 0 10px 30px rgba(241, 133, 133, 0.3);
        animation: float 3s ease-in-out infinite;
    }

    .logo-icon i {
        font-size: 2rem;
        color: white;
    }

    .logo-text {
        font-size: 1.8rem;
        font-weight: 800;
        font-family: 'Montserrat', sans-serif;
        background: var(--primary-gradient);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        margin-bottom: 0;
    }

    .form-container {
        margin-top: 1rem;
    }

    .form-header {
        text-align: center;
        margin-bottom: 2rem;
    }

    .form-header h2 {
        font-size: 1.8rem;
        color: var(--black);
        margin-bottom: 1rem;
        font-family: 'Montserrat', sans-serif;
        font-weight: 700;
    }

    .form-header p {
        color: var(--gray);
        line-height: 1.6;
        margin-bottom: 0;
    }

    .forgot-form {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        margin-bottom: 2rem;
    }

    .error-message {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        padding: 12px 16px;
        background: #fef2f2;
        border: 1px solid #fecaca;
        border-radius: 8px;
        color: #dc2626;
        font-size: 0.9rem;
        animation: slideIn 0.3s ease-out;
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
        pointer-events: none;
    }

    .input-wrapper input {
        width: 100%;
        padding: 16px 16px 16px 45px;
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

    .input-wrapper input:disabled {
        background-color: #f9fafb;
        cursor: not-allowed;
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
        min-height: 52px;
    }

    .submit-btn:hover:not(:disabled) {
        transform: translateY(-2px);
        box-shadow: 0 12px 35px rgba(241, 133, 133, 0.4);
    }

    .submit-btn:disabled {
        opacity: 0.7;
        cursor: not-allowed;
        transform: none;
    }

    .success-container {
        text-align: center;
        padding: 1rem 0;
    }

    .success-icon {
        width: 80px;
        height: 80px;
        background: linear-gradient(135deg, #10b981 0%, #059669 100%);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 0 auto 1.5rem;
        animation: scaleIn 0.5s ease-out;
    }

    .success-icon i {
        font-size: 2.5rem;
        color: white;
    }

    .success-container h2 {
        font-size: 1.8rem;
        color: var(--black);
        margin-bottom: 1rem;
        font-family: 'Montserrat', sans-serif;
        font-weight: 700;
    }

    .success-container p {
        color: var(--gray);
        line-height: 1.6;
        margin-bottom: 2rem;
    }

    .success-actions {
        display: flex;
        flex-direction: column;
        gap: 0.75rem;
    }

    .btn-primary, .btn-secondary {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 0.5rem;
        padding: 12px 20px;
        border-radius: 12px;
        font-weight: 600;
        text-decoration: none;
        transition: all 0.3s ease;
        cursor: pointer;
        border: none;
        font-size: 0.95rem;
    }

    .btn-primary {
        background: var(--primary-gradient);
        color: white;
        box-shadow: 0 4px 15px rgba(241, 133, 133, 0.3);
    }

    .btn-primary:hover {
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(241, 133, 133, 0.4);
    }

    .btn-secondary {
        background: transparent;
        color: var(--coral);
        border: 1px solid var(--coral);
    }

    .btn-secondary:hover {
        background: var(--coral);
        color: white;
    }

    .help-section {
        text-align: center;
        padding-top: 1.5rem;
        border-top: 1px solid #eee;
    }

    .help-text {
        color: var(--gray);
        font-size: 0.9rem;
        margin-bottom: 0.75rem;
    }

    .help-link {
        display: inline-flex;
        align-items: center;
        gap: 0.5rem;
        color: var(--coral);
        text-decoration: none;
        font-weight: 500;
        font-size: 0.9rem;
        transition: color 0.3s ease;
    }

    .help-link:hover {
        color: var(--deep-purple);
        text-decoration: underline;
    }

    .decorative-elements {
        position: absolute;
        inset: 0;
        pointer-events: none;
        z-index: 1;
    }

    .floating-shape {
        position: absolute;
        width: 60px;
        height: 60px;
        background: rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(10px);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 1px solid rgba(241, 133, 133, 0.2);
    }

    .floating-shape i {
        font-size: 1.5rem;
        background: var(--primary-gradient);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
    }

    .shape-1 {
        top: 15%;
        right: 10%;
        animation: float 4s ease-in-out infinite;
    }

    .shape-2 {
        bottom: 25%;
        left: 5%;
        animation: float 4s ease-in-out infinite 1.5s;
    }

    .shape-3 {
        top: 60%;
        right: 15%;
        animation: float 4s ease-in-out infinite 3s;
    }

    .bg-shapes {
        position: absolute;
        inset: 0;
        pointer-events: none;
        z-index: 0;
    }

    .bg-shapes .shape {
        position: absolute;
        border-radius: 50%;
        opacity: 0.05;
    }

    .bg-shapes .shape-1 {
        width: 250px;
        height: 250px;
        background: var(--coral);
        top: -50px;
        right: -80px;
        animation: rotate 20s linear infinite;
    }

    .bg-shapes .shape-2 {
        width: 180px;
        height: 180px;
        background: var(--deep-purple);
        bottom: -40px;
        left: -60px;
        animation: rotate 15s linear infinite reverse;
    }

    @keyframes float {
        0%, 100% {
            transform: translateY(0px) rotate(0deg);
        }
        50% {
            transform: translateY(-10px) rotate(5deg);
        }
    }

    @keyframes rotate {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }

    @keyframes slideIn {
        from {
            opacity: 0;
            transform: translateY(-10px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    @keyframes scaleIn {
        from {
            opacity: 0;
            transform: scale(0.8);
        }
        to {
            opacity: 1;
            transform: scale(1);
        }
    }

    /* Responsive */
    @media (max-width: 768px) {
        .content-wrapper {
            padding: 2rem 1.5rem;
        }

        .form-header h2 {
            font-size: 1.6rem;
        }

        .logo-text {
            font-size: 1.6rem;
        }

        .logo-icon {
            width: 60px;
            height: 60px;
        }

        .logo-icon i {
            font-size: 1.8rem;
        }

        .floating-shape {
            width: 50px;
            height: 50px;
        }

        .floating-shape i {
            font-size: 1.2rem;
        }
    }

    @media (max-width: 480px) {
        .forgot-password-page {
            padding: 1rem 0.5rem;
        }

        .content-wrapper {
            padding: 1.5rem;
        }

        .form-header h2 {
            font-size: 1.4rem;
        }

        .logo-text {
            font-size: 1.4rem;
        }

        .success-actions {
            gap: 0.5rem;
        }

        .btn-primary, .btn-secondary {
            padding: 10px 16px;
            font-size: 0.9rem;
        }

        .decorative-elements {
            display: none;
        }
    }
</style>