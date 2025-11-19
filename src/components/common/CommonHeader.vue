<template>
  <header class="site-header">
    <div class="header-inner">
      <!-- logo (왼쪽) -->
      <a href="#" class="logo" aria-label="홈으로">
        <img alt="Home Logo" src="../../assets/home_logo.png" />
      </a>

      <!-- 데스크탑/태블릿 메뉴 -->
      <nav class="nav-menu" :class="{ open: menuOpen }" aria-label="주요메뉴">
        <a href="#" class="nav-link">My HF</a>
        <a href="#" class="nav-link">신청</a>
        <a href="#" class="nav-link">간편 서류제출</a>
        <a href="#" class="nav-link">고객서비스</a>
      </nav>

      <!-- 로그인 버튼 (항상 우측 상단에 위치) -->
      <a href="#" class="login-btn" @click.prevent="onLoginClick">{{ isLoggedIn ? '로그아웃' : '로그인' }}</a>

      <!-- 모바일 햄버거 (작은 화면에서만 보임) -->
      <button class="burger" @click="toggleMenu" :aria-expanded="menuOpen" aria-label="메뉴 열기 닫기">
        <span class="burger-line" />
        <span class="burger-line" />
        <span class="burger-line" />
      </button>
    </div>

    <!-- 모바일: 메뉴가 열렸을 때 보이는 드롭다운 (슬라이드) -->
    <transition name="slide-fade">
      <div v-if="menuOpen" class="mobile-menu" @click.self="closeMenu">
        <nav class="mobile-nav">
          <a href="#" class="mobile-link" @click="closeMenu">My HF</a>
          <a href="#" class="mobile-link" @click="closeMenu">신청</a>
          <a href="#" class="mobile-link" @click="closeMenu">간편 서류제출</a>
          <a href="#" class="mobile-link" @click="closeMenu">고객서비스</a>
        </nav>
      </div>
    </transition>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      menuOpen: false,
      // 실제 로그인 상태 연동 전에는 임시 변수로 사용 가능
      isLoggedIn: false
    };
  },
  methods: {
    toggleMenu() {
      this.menuOpen = !this.menuOpen;
    },
    closeMenu() {
      this.menuOpen = false;
    },
    onLoginClick() {
      // 여기에서 실제 인증 로직을 연결하세요.
      // 현재는 데모용으로 상태 토글 처리.
      this.isLoggedIn = !this.isLoggedIn;
      // 메뉴 닫기 (모바일에서 로그인 누르면 메뉴 닫히게)
      this.closeMenu();
    }
  }
};
</script>

<style scoped>
/* 기본 리셋/타이포 */
.site-header {
  width: 100%;
  background: #ffffff;
  box-shadow: 0 2px 10px rgba(0,0,0,0.06);
  position: relative;
  z-index: 50;
}

.header-inner {
  max-width: 1280px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  position: relative; /* 절대 위치 요소 기준 */
  padding: 12px 20px;
  gap: 20px;
}

/* 로고 */
.logo img {
  width: 200px;
  height: auto;
  display: block;
  user-select: none;
}

/* 내비게이션 (데스크탑) */
.nav-menu {
  display: flex;
  gap: 32px;
  margin-left: 32px; /* 로고와 메뉴 사이 간격 */
  align-items: center;
  flex: 1 1 auto; /* 남은 공간 차지 */
}

/* 각 링크 스타일 */
.nav-link {
  font-size: 16px;
  font-weight: 600;
  color: #333333;
  text-decoration: none; /* 밑줄 제거 */
  padding: 6px 0;
  transition: color .18s, transform .12s;
  border-radius: 4px;
  outline: none;
}
.nav-link:hover,
.nav-link:focus {
  color: #005bbf;
  transform: translateY(-1px);
}

/* 로그인 버튼 (우측 상단) */
.login-btn {
  position: absolute;
  right: 20px;
  top: 12px;
  font-size: 15px;
  font-weight: 700;
  padding: 8px 16px;
  border-radius: 10px;
  background: #005bbf;
  color: #fff;
  text-decoration: none;
  transition: background .18s, transform .12s;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
.login-btn:hover,
.login-btn:focus {
  background: #004a9a;
  transform: translateY(-1px);
}

/* 햄버거 (mobile) */
.burger {
  display: none;
  margin-left: auto;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 8px;
  border-radius: 8px;
}
.burger:focus { outline: 2px solid rgba(0,91,191,0.2) }

.burger-line {
  display: block;
  width: 22px;
  height: 2px;
  background: #333;
  margin: 4px 0;
  border-radius: 2px;
}

/* 모바일 메뉴 드롭다운 (슬라이드), 화면 전체 너비 사용 */
.mobile-menu {
  width: 100%;
  background: #ffffff;
  box-shadow: 0 8px 20px rgba(0,0,0,0.08);
}
.mobile-nav {
  display: flex;
  flex-direction: column;
  padding: 10px 20px 18px 20px;
  gap: 6px;
}
.mobile-link {
  display: block;
  padding: 12px 10px;
  font-weight: 700;
  color: #222;
  text-decoration: none;
  border-radius: 8px;
}
.mobile-link:hover,
.mobile-link:focus {
  background: rgba(0,91,191,0.06);
  color: #005bbf;
}

/* 슬라이드 트랜지션 */
.slide-fade-enter-active {
  transition: all 220ms ease;
}
.slide-fade-leave-active {
  transition: all 180ms ease;
}
.slide-fade-enter-from {
  transform: translateY(-6px);
  opacity: 0;
}
.slide-fade-enter-to {
  transform: translateY(0);
  opacity: 1;
}
.slide-fade-leave-from {
  transform: translateY(0);
  opacity: 1;
}
.slide-fade-leave-to {
  transform: translateY(-6px);
  opacity: 0;
}

/* -----------------
   반응형 브레이크포인트
   ----------------- */

/* 큰 화면 (데스크탑) 기본 스타일은 이미 적용 */

/* 테블릿 이하: 네비게이션 간격 줄임 */
@media (max-width: 1024px) {
  .nav-menu { gap: 24px; }
  .logo img { width: 180px; }
}

/* 모바일: 네비게이션 숨기고 햄버거 노출, 로그인 버튼은 우측 상단 고정 */
@media (max-width: 768px) {
  .nav-menu {
    display: none; /* 데스크탑 메뉴 숨김 */
  }
  .burger {
    display: inline-flex;
    position: absolute;
    right: 64px; /* 로그인 버튼과 겹치지 않게 조정 */
    top: 12px;
  }

  /* 로그인 버튼을 더 오른쪽으로 밀어서 햄버거와 간격 확보 */
  .login-btn {
    right: 16px;
    top: 10px;
    padding: 7px 12px;
  }
}

/* 초소형 모바일 (좁은 화면) */
@media (max-width: 420px) {
  .logo img { width: 150px; }
  .burger { right: 56px; }
  .login-btn { padding: 6px 10px; font-size: 14px; }
}
</style>
