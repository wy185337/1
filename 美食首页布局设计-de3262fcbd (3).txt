// 轮播图逻辑
document.addEventListener('DOMContentLoaded', function() {
    const carouselItems = document.querySelectorAll('.carousel-item');
    const indicators = document.querySelectorAll('.carousel-indicator');
    let currentIndex = 0;

    function showSlide(index) {
        carouselItems.forEach((item, i) => {
            item.style.opacity = i === index ? '1' : '0';
        });

        indicators.forEach((indicator, i) => {
            if (i === index) {
                indicator.classList.add('bg-opacity-100');
                indicator.classList.remove('bg-opacity-50');
            } else {
                indicator.classList.add('bg-opacity-50');
                indicator.classList.remove('bg-opacity-100');
            }
        });
    }

    function nextSlide() {
        currentIndex = (currentIndex + 1) % carouselItems.length;
        showSlide(currentIndex);
    }

    // 初始显示第一张
    showSlide(currentIndex);

    // 自动轮播
    setInterval(nextSlide, 5000);

    // 点击指示器切换
    indicators.forEach((indicator, index) => {
        indicator.addEventListener('click', () => {
            currentIndex = index;
            showSlide(currentIndex);
        });
    });

    // 移动端菜单切换
    const mobileMenuBtn = document.getElementById('mobileMenuBtn');
    const mobileMenu = document.getElementById('mobileMenu');
    if (mobileMenuBtn && mobileMenu) {
        mobileMenuBtn.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });
    }

    // 登录/注册模态框逻辑
    const loginBtn = document.getElementById('loginBtn');
    const registerBtn = document.getElementById('registerBtn');
    const loginModal = document.getElementById('loginModal');
    const registerModal = document.getElementById('registerModal');
    const closeLoginModal = document.getElementById('closeLoginModal');
    const closeRegisterModal = document.getElementById('closeRegisterModal');
    const switchToRegister = document.getElementById('switchToRegister');
    const switchToLogin = document.getElementById('switchToLogin');

    if (loginBtn && loginModal) {
        loginBtn.addEventListener('click', () => {
            loginModal.classList.remove('hidden');
        });
    }

    if (registerBtn && registerModal) {
        registerBtn.addEventListener('click', () => {
            registerModal.classList.remove('hidden');
        });
    }

    if (closeLoginModal && loginModal) {
        closeLoginModal.addEventListener('click', () => {
            loginModal.classList.add('hidden');
        });
    }

    if (closeRegisterModal && registerModal) {
        closeRegisterModal.addEventListener('click', () => {
            registerModal.classList.add('hidden');
        });
    }

    if (switchToRegister && loginModal && registerModal) {
        switchToRegister.addEventListener('click', () => {
            loginModal.classList.add('hidden');
            registerModal.classList.remove('hidden');
        });
    }

    if (switchToLogin && registerModal && loginModal) {
        switchToLogin.addEventListener('click', () => {
            registerModal.classList.add('hidden');
            loginModal.classList.remove('hidden');
        });
    }

    // 点击模态框外部关闭
    window.addEventListener('click', (e) => {
        if (e.target === loginModal) {
            loginModal.classList.add('hidden');
        }
        if (e.target === registerModal) {
            registerModal.classList.add('hidden');
        }
    });

    // 可选：阻止表单默认跳转，实际开发中你可能要用AJAX
    document.querySelectorAll('#loginModal form, #registerModal form').forEach(form => {
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            // 这里可加入真实的登录或注册逻辑
        });
    });
});