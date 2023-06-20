<template>
  <footer class="p-footer">
    <div class="p-footer__inner l-footer">
      <div class="p-footer__menu">
        <div class="p-footer__menu__head">
          <NuxtLink to="/">
            <img
              :src="$config.baseURL + '/files/user/images/logo_wh.svg'"
              alt="RCMS テンプレート"
            />
          </NuxtLink>
        </div>
        <div class="p-footer__menu__body">
          <ul>
            <li>
              <NuxtLink to="/"
                ><i
                  class="p-footer__menu__icon fas fa-angle-right"
                  aria-hidden="true"
                ></i
                >トップ</NuxtLink
              >
            </li>
            <li>
              <NuxtLink to="/privacy/"
                ><i
                  class="p-footer__menu__icon fas fa-angle-right"
                  aria-hidden="true"
                ></i
                >プライバシーポリシー</NuxtLink
              >
            </li>
            <li>
              <NuxtLink to="/sitemap/"
                ><i
                  class="p-footer__menu__icon fas fa-angle-right"
                  aria-hidden="true"
                ></i
                >サイトマップ</NuxtLink
              >
            </li>
          </ul>
          <ul>
            <li>
              <a href="" target="_blank" rel="noopener noreferrer"
                ><i class="fab fa-facebook-square fa-2x" aria-hidden="true"></i
              ></a>
            </li>
            <li>
              <a href="" target="_blank" rel="noopener noreferrer"
                ><i class="fab fa-twitter-square fa-2x" aria-hidden="true"></i
              ></a>
            </li>
            <li>
              <a href="" target="_blank" rel="noopener noreferrer"
                ><i class="fab fa-instagram fa-2x" aria-hidden="true"></i
              ></a>
            </li>
            <li>
              <a href="" target="_blank" rel="noopener noreferrer"
                ><i class="fab fa-youtube fa-2x" aria-hidden="true"></i
              ></a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="p-footer__copyright">
      Copyright(c) {{ new Date().getFullYear() }} * All Rights Reserved. managed
      by
      <a href="https://kuroco.app/ja/" rel="nofollow">Kuroco</a>
    </div>
  </footer>
</template>

<script>
export default {};
</script>
