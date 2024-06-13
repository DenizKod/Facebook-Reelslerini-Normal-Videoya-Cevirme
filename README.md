# REELSLERI-NORMAL-VIDEO-YAPMA

### ADIM 1

<p>- Tampermonkey eklentisi tarayıcınıza ekleyin</p>
<p>- Yeni Betik oluştura tıklayın</p>

![image](https://github.com/DenizKod/ARK-ISTEGI-IPTAL-ETME/assets/168285638/7e1b2696-803e-447a-ae3f-f7844a44d28f)

#### Aşağıdaki kodu betik oluşturma sayfasına yapıştırıp betiği kaydedin

```
// ==UserScript==
// @name        Facebook Reels Zaman Butonu Ekleme
// @namespace   UserScript
// @match       https://www.facebook.com/*
// @version     0.1.2
// @license     MIT
// @author      Deniz Gölcü BGY
// @description Facebook Reels Zaman Butonu Ekleme
// @run-at      document-start
// @grant       none
// @unwrap
// @downloadURL https://update.greasyfork.org/scripts/487657/Facebook%20Reel%3A%20Video%20Controls%20Fork.user.js
// @updateURL https://update.greasyfork.org/scripts/487657/Facebook%20Reel%3A%20Video%20Controls%20Fork.meta.js
// ==/UserScript==

document.addEventListener('play', (evt) => {
  const target = (evt || 0).target;

  if (target instanceof HTMLVideoElement && !target.hasAttribute('controls') && location.href.includes('reel')) {
    let buttonLayer = target.closest('div[class][role="button"][tabindex]');

    if (buttonLayer) {
      target.setAttribute('controls', '');

      setTimeout(() => {
        Object.assign(target.style, {
          'position': 'relative',
          'zIndex': 999,
          'pointerEvents': 'all'
        });

        [...buttonLayer.querySelectorAll('.x10l6tqk.x13vifvy:not(.x1m3v4wt)')].forEach(s => {
          Object.assign(s.style, {
            'pointerEvents': 'none',
            'position': 'relative',
            'zIndex': 1000
          });
        });
      }, 1);
    }
  }
}, true);
```

## Facebook sayfasını bir kere yenileyin. artık bundan sonra tüm reels'lere tıklayınca zaman yönetme butonu aktif olacak.
