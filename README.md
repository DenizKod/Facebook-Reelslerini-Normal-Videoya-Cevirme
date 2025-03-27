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
// @version     0.1.4
// @license     MIT
// @author      Deniz Gölcü BGY
// @description Facebook Reels Zaman Butonu Ekleme
// @run-at      document-start
// @grant       none
// @unwrap
// @downloadURL https://update.greasyfork.org/scripts/487657/Facebook%20Reel%3A%20Video%20Controls%20Fork.user.js
// @updateURL   https://update.greasyfork.org/scripts/487657/Facebook%20Reel%3A%20Video%20Controls%20Fork.meta.js
// ==/UserScript==

document.addEventListener('play', (evt) => {
    const target = evt.target;

    if (target instanceof HTMLVideoElement && !target.hasAttribute('controls') && location.href.includes('reel')) {
        let buttonLayer = target.closest('div[class*="x9f619"][class*="x1n2onr6"]');

        if (buttonLayer) {
            target.setAttribute('controls', '');

            setTimeout(() => {
                Object.assign(target.style, {
                    'position': 'relative',
                    'zIndex': 999,
                    'pointerEvents': 'all'
                });

                // Yalnızca Yorum Yap, Beğen, Paylaş ve Diğer Videoya Geç butonlarını aktif hale getir
                const interactiveButtons = buttonLayer.querySelectorAll('[aria-label="Yorum Yap"], [aria-label="Beğen"], [aria-label="Paylaş"], .x14yjl9h');
                interactiveButtons.forEach(button => {
                    Object.assign(button.style, {
                        'pointerEvents': 'auto',
                        'zIndex': 1002
                    });
                });

                // Diğer tüm üst katmanları devre dışı bırak
                [...buttonLayer.children].forEach(child => {
                    if (![...interactiveButtons].includes(child)) {
                        Object.assign(child.style, {
                            'pointerEvents': 'none'
                        });
                    }
                });

            }, 1);
        }
    }
}, true);

// Yeni içerik yüklendiğinde butonları tekrar aktif et
const observer = new MutationObserver(() => {
    document.querySelectorAll('video').forEach(video => {
        if (!video.hasAttribute('controls')) {
            video.dispatchEvent(new Event('play'));
        }
    });
});

observer.observe(document.body, { childList: true, subtree: true });
```

## Facebook sayfasını bir kere yenileyin. artık bundan sonra tüm reels'lere tıklayınca zaman yönetme butonu aktif olacak.
