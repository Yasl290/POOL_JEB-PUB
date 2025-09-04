<script>
    import { createEventDispatcher } from 'svelte';

    export let loading = false;
    export let error = '';

    let email = '';
    let password = '';
    let rememberMe = false;

    const dispatch = createEventDispatcher();

    function handleSubmit() {
        if (!email || !password) {
            dispatch('error', 'Veuillez remplir tous les champs');
            return;
        }

        dispatch('submit', {
            email,
            password,
            rememberMe
        });
    }

    function handleSocialLogin(provider) {
        dispatch('socialLogin', provider);
    }
</script>

<div class="login-form-container">
    <!-- En-tête -->
    <div class="form-header">
        <h2>Connexion</h2>
        <p>Accédez à votre espace personnel</p>
    </div>

    <!-- Connexions sociales -->
    <div class="social-login">
        <button
                type="button"
                class="social-btn google-btn"
                on:click={() => handleSocialLogin('google')}
                disabled={loading}
        >
            <i class="fab fa-google"></i>
            <span>Continuer avec Google</span>
        </button>
        <button
                type="button"
                class="social-btn linkedin-btn"
                on:click={() => handleSocialLogin('linkedin')}
                disabled={loading}
        >
            <i class="fab fa-linkedin"></i>
            <span>Continuer avec LinkedIn</span>
        </button>
    </div>

    <div class="divider">
        <span>ou</span>
    </div>

    <!-- Formulaire -->
    <form on:submit|preventDefault={handleSubmit} class="login-form">
        {#if error}
            <div class="error-message" role="alert">
                <i class="fas fa-exclamation-triangle"></i>
                <span>{error}</span>
            </div>
        {/if}

        <div class="form-group">
            <label for="login-email">Adresse e-mail</label>
            <div class="input-wrapper">
                <i class="fas fa-envelope" aria-hidden="true"></i>
                <input
                        id="login-email"
                        type="email"
                        bind:value={email}
                        placeholder="votre@email.com"
                        required
                        disabled={loading}
                        autocomplete="email"
                />
            </div>
        </div>

        <div class="form-group">
            <label for="login-password">Mot de passe</label>
            <div class="input-wrapper">
                <i class="fas fa-lock" aria-hidden="true"></i>
                <input
                        id="login-password"
                        type="password"
                        bind:value={password}
                        placeholder="Votre mot de passe"
                        required
                        disabled={loading}
                        autocomplete="current-password"
                />
            </div>
        </div>

        <div class="form-options">
            <label class="checkbox-wrapper">
                <input
                        type="checkbox"
                        bind:checked={rememberMe}
                        disabled={loading}
                />
                <span class="checkmark"></span>
                <span class="checkbox-label">Se souvenir de moi</span>
            </label>
            <a href="/forgot-password" class="forgot-link">Mot de passe oublié ?</a>
        </div>

        <button type="submit" class="submit-btn" disabled={loading} class:loading>
            {#if loading}
                <i class="fas fa-spinner fa-spin" aria-hidden="true"></i>
                <span>Connexion...</span>
            {:else}
                <i class="fas fa-sign-in-alt" aria-hidden="true"></i>
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

<style>
    .login-form-container {
        width: 100%;
        max-width: 400px;
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
        font-family: 'Montserrat', sans-serif;
        font-weight: 800;
    }

    .form-header p {
        color: var(--gray);
        margin-bottom: 0;
        font-size: 1rem;
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
        font-size: 0.95rem;
        transition: all 0.3s ease;
        cursor: pointer;
    }

    .social-btn:hover:not(:disabled) {
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
    }

    .social-btn:disabled {
        opacity: 0.6;
        cursor: not-allowed;
    }

    .google-btn {
        color: #db4437;
        border-color: #db4437;
    }

    .google-btn:hover:not(:disabled) {
        background: #db4437;
        color: white;
    }

    .linkedin-btn {
        color: #0077b5;
        border-color: #0077b5;
    }

    .linkedin-btn:hover:not(:disabled) {
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
        background: #fef2f2;
        border: 1px solid #fecaca;
        border-radius: 8px;
        color: #dc2626;
        font-size: 0.9rem;
        animation: slideIn 0.3s ease-out;
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

    .input-wrapper input:disabled {
        background-color: #f9fafb;
        cursor: not-allowed;
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
        color: var(--black);
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
        flex-shrink: 0;
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

    .checkbox-wrapper input[type="checkbox"]:disabled + .checkmark {
        opacity: 0.5;
        cursor: not-allowed;
    }

    .forgot-link {
        color: var(--coral);
        font-size: 0.9rem;
        text-decoration: none;
        font-weight: 500;
        transition: color 0.3s ease;
    }

    .forgot-link:hover {
        color: var(--deep-purple);
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

    .submit-btn.loading {
        pointer-events: none;
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
        font-size: 0.95rem;
    }

    .register-link {
        color: var(--coral);
        font-weight: 600;
        text-decoration: none;
        transition: color 0.3s ease;
    }

    .register-link:hover {
        color: var(--deep-purple);
        text-decoration: underline;
    }

    /* Responsive */
    @media (max-width: 768px) {
        .form-header h2 {
            font-size: 1.8rem;
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

    @media (max-width: 480px) {
        .login-form-container {
            max-width: 100%;
        }

        .social-login {
            gap: 0.5rem;
        }

        .social-btn span {
            display: none;
        }

        .social-btn {
            justify-content: center;
            min-width: 48px;
        }
    }
</style>