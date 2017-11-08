---

layout: yandex2

style: |
    .center {
        text-align: center;
    }
    
    .center img {
        margin: 0 auto;
    }

    .video-container {
        height: 90%;
        text-align: center;
    }
    
    .video {
        height: 100%;
    }
---

# ![](themes/yandex2/images/logo-{{ site.presentation.lang }}.svg){:.logo}

## {{ site.presentation.title }}
{:.title}

### ![](themes/yandex2/images/title-logo-{{ site.presentation.lang }}.svg){{ site.presentation.service }}

{% if site.presentation.nda %}
![](themes/yandex2/images/title-nda.svg)
{:.nda}
{% endif %}

<div class="authors">
{% if site.author %}
<p>{{ site.author.name }}{% if site.author.position %}, {{ site.author.position }}{% endif %}</p>
{% endif %}

{% if site.author2 %}
<p>{{ site.author2.name }}{% if site.author2.position %}, {{ site.author2.position }}{% endif %}</p>
{% endif %}

</div>

## Поисковая выдача
{:.section}

### Наш проект

## SERP (Search Engine Result Page)
{:.section}

### Наш проект

## SERP

**Одна страница**

**Большая вариативность**

**Больше 50 разработчиков**

## SERP

<div class="video-container">
    <video class="video" autoplay loop>
        <source src="serp-screens/movie.mp4">
    </video>
</div>

## Как мы работаем?
{:.section}

## Колесо скорости
{:.images .center}

![](diagrams/velocity-cycle.svg)

## Онлайн-измерения

RUM – real user measurement

**Navigation Timing API**

**Resource Timing API**

**Paint Timing API**

**High Resolution Time – собственные таймеры**

## Navigation Timing API

```js
const tm = performance.timing
const loadMetrics = {
    wait: tm.domainLookupStart - tm.navigationStart,
    dns: tm.domainLookupEnd - tm.domainLookupStart,
    tcp: tm.connectEnd - tm.connectStart,
    tls: tm.connectEnd - tm.secureConnectionStart,
    ttfb: tm.responseStart - tm.connectEnd,
    download: tm.responseEnd - tm.responseStart,
    domLoading: tm.domLoading - tm.responseStart,
    domInteractive: tm.domInteractive - tm.responseStart,
    domLoaded: tm.domContentLoadedEventStart - tm.responseStart,
    domInit: tm.domContentLoadedEventEnd - tm.domContentLoadedEventStart,
}
```

## Resource Timing API

```js
const entry = performance.getEntriesByName('https://yastatic.net/jquery.js')[0]
const resTiming = {
    cacheHit: entry.transferSize === 0,
    wait: entry.domainLookupStart - entry.startTime,
    dns: entry.domainLookupEnd - entry.domainLookupStart,
    // …
    transferSize: entry.transferSize,
    duration: entry.duration,
}
```

## Paint Timing API

```js
function getFirstPaintTime() {
    const paints = performance.getEntriesByType('paint')
    for (let paint of paints) {
        if (paint.name === 'first-contentful-paint') {
            return paint.startTime  
        }
    }
}
```

## Кастомные API для первой отрисовки

```js
function getFirstPaintTime() {
    if (typeof chrome !== 'undefined' && typeof chrome.loadTimes === 'function') {
        return chrome.loadTimes().firstPaintTime * 1000
    }

    if ('msFirstPaint' in performance.timing) {
        return performance.timing.msFirstPaint
    }
}
```

## Таймеры

```js
BEM.channel('i-bem').onFirst('init', () => {
    Rum.sendTimeMark('client-framework-inited', performance.now())
})
```

## Оценка отрисовки контента

```html
<script>
requestAnimationFrame(() => {
    Rum.sendTimeMark('content-paint-low', performance.now())
    requestAnimationFrame(() => {
        Rum.sendTimeMark('content-paint-high', performance.now())
    })
})
</script>
<div class="content">Hello, world!</div>
```

## АБ-тестирование

|  Метрика                 |  Контроль, мс    | Эксперимент, мс |     Δ, мс |  MW-тест, % |
+--------------------------|------------------|-----------------|-----------|-------------+
|  TTFB                    |  380             |  375            |  -5       |  20         |
|  TTFP                    |  420             |  450            |  30       |  50         |
|  Download                |  878             |  932            |  54       |  **99.5**   |
|  Cont. paint low         |  900             |  950            |  50       |  **100**    |
|  Cont. paint high        |  1000            |  1100           |  100      |  98         |
|  Main.JS duration        |  300             |  400            |  100      |  **100**    |
|  JS inited               |  1200            |  1400           |  200      |  **99.9**   |


## Офлайн-измерения

|  Метрика                      |  База    | Пулл-реквест  |     Δ     |
+-------------------------------|----------|---------------|-----------|
|  Размер html, Кб (gzip)       |  80.2    |  100.2        |  **20**   |
|  Размер AJAX JSON, Кб  (gzip) |  15.3    |  15.8         |  0.5      |
|  Размер main.js, Кб  (br)     |  90      |  95           |  **5**    |
|  Размер main.css, Кб  (br)    |  15.4    |  15.4         |  0        |
|  Время шаблонизации html, мс  |  123     |  126          |  3        |
|  Время создания AJAX JSON, мс |  84      |  85           |  1        |


## Контакты 
{:.contacts}

{% if site.author %}

<figure markdown="1">

### {{ site.author.name }}

{% if site.author.position %}
{{ site.author.position }}
{% endif %}

</figure>

{% endif %}

{% if site.author2 %}

<figure markdown="1">

### {{ site.author2.name }}

{% if site.author2.position %}
{{ site.author2.position }}
{% endif %}

</figure>

{% endif %}

<!-- разделитель контактов -->
-------

<!-- left -->
- {:.github}andre487
- {:.mail}andre487@yandex-team.ru
- {:.twitter}@andre487

<!-- right -->
- {:.phone}Nexus 5X
- {:.telegram}andre487

<!-- 

- {:.mail}andre487@yandex-team.ru
- {:.phone}Nexus 5X
- {:.github}andre487
- {:.twitter}@author
- {:.telegram}author
- {:.skype}author
- {:.instagram}author
- {:.facebook}author
- {:.vk}@author
- {:.ok}@author

-->
