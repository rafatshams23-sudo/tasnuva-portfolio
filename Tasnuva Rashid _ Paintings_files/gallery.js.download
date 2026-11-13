const gallery = document.querySelector('#gallery');
const viewer = document.querySelector('dialog');
const artwork = viewer.querySelector('img');
const title = viewer.querySelector('h3');
let active = 0;
let opener;

document.querySelector('#count').textContent = `${paintings.length} works`;

function show(index) {
  active = (index + paintings.length) % paintings.length;
  const work = paintings[active];
  artwork.src = work.src;
  artwork.alt = work.title;
  title.textContent = work.title;
}

paintings.forEach((work, index) => {
  const button = document.createElement('button');
  button.type = 'button';
  button.className = 'work';
  button.innerHTML = '<span class="mount"><img loading="lazy" decoding="async" alt=""></span><span class="work-title"><bdi></bdi><span aria-hidden="true">↗</span></span>';
  button.querySelector('img').src = work.src;
  button.querySelector('bdi').textContent = work.title;
  button.addEventListener('click', () => {
    opener = button;
    show(index);
    viewer.showModal();
  });
  gallery.append(button);
});

viewer.querySelector('.close').addEventListener('click', () => viewer.close());
viewer.querySelector('#previous').addEventListener('click', () => show(active - 1));
viewer.querySelector('#next').addEventListener('click', () => show(active + 1));
viewer.addEventListener('close', () => opener?.focus());
viewer.addEventListener('click', event => {
  if (event.target === viewer) viewer.close();
});
viewer.addEventListener('keydown', event => {
  if (event.key === 'ArrowLeft') show(active - 1);
  if (event.key === 'ArrowRight') show(active + 1);
});

const hero = document.querySelector('.hero');
const feature = hero.querySelector('.feature img');
const caption = hero.querySelector('figcaption');
const thumbs = hero.querySelector('.thumbs');
const featuredTitles = ['After the Rain', 'Ripples', 'Blues and Roots', 'Bound, Yet Blue Me', 'Mirrors', 'Penance'];

function alignHeroBackground() {
  document.body.style.setProperty('--hero-height', `${hero.offsetTop + hero.offsetHeight}px`);
}

for (const name of featuredTitles) {
  const work = paintings.find(item => item.title === name);
  if (!work) continue;
  const button = document.createElement('button');
  const thumbnail = document.createElement('img');
  thumbnail.src = work.src;
  thumbnail.alt = '';
  button.type = 'button';
  button.setAttribute('aria-label', `Show ${name}`);
  button.setAttribute('aria-pressed', String(name === caption.textContent));
  button.append(thumbnail);
  button.addEventListener('click', () => {
    thumbs.querySelector('[aria-pressed=true]')?.setAttribute('aria-pressed', 'false');
    button.setAttribute('aria-pressed', 'true');
    feature.src = work.src;
    feature.alt = work.title;
    caption.textContent = name;
  });
  thumbs.append(button);
}

new ResizeObserver(alignHeroBackground).observe(hero);
alignHeroBackground();
